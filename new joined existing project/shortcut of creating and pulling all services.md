Here’s a clean **README documentation** you can use for your scripts.

---

# README.md

````markdown
# Multi-Repo Git Automation Scripts

This folder contains Bash scripts to manage multiple Git repositories inside one root directory.

These scripts are useful when you have many microservices and want to:

- convert Git remotes from SSH to HTTPS
- create the same feature branch in all services
- pull the latest `main` branch into your feature branch across all services

---

## Project Structure

Run these scripts from the **root folder** where all service folders exist.

Example:

```bash
/d/nanosoft/pksf
├── convert-ssh-to-https-all.sh
├── create-branch-all.sh
├── pull-main-all.sh
├── pksf-imis-auth-service/
├── pksf-imis-loan-management-service/
├── pksf-imis-project-service/
└── ...
````

---

## Prerequisites

Before using these scripts, make sure:

* Git is installed
* Git Bash is installed (for Windows)
* All service folders are Git repositories
* You have access to all repositories
* You are running the scripts from the root folder

Check Git:

```bash
git --version
```

---

## 1. convert-ssh-to-https-all.sh

### Purpose

This script converts Git remote URLs from **SSH** format to **HTTPS** format for all repositories inside the current root folder.

### Why use this?

If you get SSH errors like:

```bash
ssh: connect to host github.com port 22: Connection timed out
fatal: Could not read from remote repository.
```

then switching to HTTPS usually fixes the issue.

### Script

```bash
#!/bin/bash

echo "Converting Git remotes from SSH to HTTPS for all services..."

for dir in */; do
  if [ -d "$dir/.git" ]; then
    cd "$dir" || continue

    url=$(git remote get-url origin 2>/dev/null)

    if [[ -z "$url" ]]; then
      echo "Skipping ${dir%/} (no origin remote)"
      cd ..
      continue
    fi

    if [[ "$url" == git@github.com:* ]]; then
      new_url=$(echo "$url" | sed 's#git@github.com:#https://github.com/#')
      echo "Updating ${dir%/}"
      git remote set-url origin "$new_url"
      git remote -v
    else
      echo "Skipping ${dir%/} (already HTTPS)"
    fi

    cd ..
  fi
done

echo "Done."
```

### Run

```bash
chmod +x convert-ssh-to-https-all.sh
./convert-ssh-to-https-all.sh
```

### Output Example

```bash
Updating pksf-imis-auth-service
Updating pksf-imis-loan-management-service
Skipping pksf-imis-project-service (already HTTPS)
Done.
```

---

## 2. create-branch-all.sh

### Purpose

This script creates and pushes the same feature branch in all repositories.

### What it does

For each repository:

1. fetches latest remote changes
2. checks out `main`
3. pulls latest `origin/main`
4. checks whether the feature branch already exists locally
5. checks whether the feature branch exists remotely
6. if branch does not exist, creates it from `main`
7. pushes the branch to remote if newly created

### Script

```bash
#!/bin/bash

BRANCH="feature/saddamnvn"

echo "Creating and pushing $BRANCH in all services..."

for dir in */ ; do
    if [ -d "$dir/.git" ]; then
        echo
        echo "Processing ${dir%/}"
        cd "$dir" || continue

        git fetch origin || { echo "Fetch failed in ${dir%/}"; cd ..; continue; }

        git checkout main || git checkout -b main origin/main
        git pull origin main || { echo "Pull main failed in ${dir%/}"; cd ..; continue; }

        if git show-ref --verify --quiet "refs/heads/$BRANCH"; then
            echo "Local branch already exists"
            git checkout "$BRANCH"
        elif git ls-remote --heads origin "$BRANCH" | grep -q "$BRANCH"; then
            echo "Remote branch exists, creating local tracking branch"
            git checkout -b "$BRANCH" "origin/$BRANCH"
        else
            echo "Creating and pushing new branch from main"
            git checkout -b "$BRANCH"
            git push -u origin "$BRANCH" || { echo "Push failed in ${dir%/}"; cd ..; continue; }
        fi

        cd ..
    fi
done

echo
echo "Done."
```

### Run

```bash
chmod +x create-branch-all.sh
./create-branch-all.sh
```

### Use Case

Run this script:

* the first time you set up your feature branch
* when a new repository is added later
* when your branch does not yet exist in some services

---

## 3. pull-main-all.sh

### Purpose

This script pulls the latest `main` branch into your feature branch across all repositories.

### What it does

For each repository:

1. fetches latest changes from origin
2. checks out your feature branch
3. pulls latest `origin/main` into that feature branch

### Script

```bash
#!/bin/bash

BRANCH="feature/saddamnvn"

echo "Pulling latest main into $BRANCH for all services..."

for dir in */ ; do
    if [ -d "$dir/.git" ]; then
        echo
        echo "Processing ${dir%/}"
        cd "$dir" || continue

        git fetch origin || { echo "Fetch failed in ${dir%/}"; cd ..; continue; }
        git checkout "$BRANCH" || { echo "Branch missing in ${dir%/}"; cd ..; continue; }
        git pull origin main || echo "Pull failed in ${dir%/}"

        cd ..
    fi
done

echo
echo "Done."
```

### Run

```bash
chmod +x pull-main-all.sh
./pull-main-all.sh
```

### Use Case

Run this script daily:

* before starting work
* after teammates push new code to `main`
* when you want to sync all services with latest `main`

---

## Recommended Workflow

### First Time Setup

Run these commands once:

```bash
./convert-ssh-to-https-all.sh
./create-branch-all.sh
```

### Daily Workflow

Run this whenever you want the latest code from `main`:

```bash
./pull-main-all.sh
```

### If a New Service Is Added

Run:

```bash
./create-branch-all.sh
```

Then continue daily with:

```bash
./pull-main-all.sh
```

---

## Branch Configuration

Current feature branch used in the scripts:

```bash
feature/saddamnvn
```

If you want to use another branch, update this line in both scripts:

```bash
BRANCH="feature/saddamnvn"
```

Example:

```bash
BRANCH="feature/new-branch-name"
```

---

## Common Errors and Fixes

### 1. SSH timeout error

Error:

```bash
ssh: connect to host github.com port 22: Connection timed out
fatal: Could not read from remote repository.
```

Fix:

```bash
./convert-ssh-to-https-all.sh
```

---

### 2. Branch missing in some repos

Error:

```bash
Branch missing in repo-name
```

Fix:

```bash
./create-branch-all.sh
```

---

### 3. Permission denied when running script

Fix:

```bash
chmod +x script-name.sh
```

Or run with:

```bash
bash script-name.sh
```

---

### 4. Script run from wrong folder

These scripts must be run from the parent folder containing all repositories.

Correct:

```bash
cd /d/nanosoft/pksf
./pull-main-all.sh
```

Wrong:

```bash
cd /d/nanosoft/pksf/pksf-imis-auth-service
./pull-main-all.sh
```

---

## Best Practices

* Always run scripts from the root folder
* Use HTTPS if SSH connection is unstable
* Run `create-branch-all.sh` once before using `pull-main-all.sh`
* Run `pull-main-all.sh` regularly to stay updated
* Review output for any failed repositories

---

## Quick Commands Summary

### Convert remotes to HTTPS

```bash
./convert-ssh-to-https-all.sh
```

### Create and push feature branch in all repos

```bash
./create-branch-all.sh
```

### Pull latest main into feature branch in all repos

```bash
./pull-main-all.sh
```

---

## Author

Created for multi-repository microservice workflow automation using Git Bash.

```

---

If you want, I can also give you:
1. a **short professional README**
2. a **better formatted enterprise README**
3. :contentReference[oaicite:0]{index=0}
```
