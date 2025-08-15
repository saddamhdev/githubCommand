Alright — let’s walk through starting a **merge** again from your existing GitHub project.

Since you’re currently on `main` and up to date, you’ll first want a separate branch to merge.


https://www.youtube.com/watch?v=7B_km8LrkJw

<img width="852" height="427" alt="image" src="https://github.com/user-attachments/assets/19877518-9cd4-40c8-8a20-6949a97fa089" />

---

## 1️⃣ Create a feature branch and make a change

```bash
# Make sure you're on main and synced
git switch main
git pull origin main

# Create a feature branch
git switch -c feature/demo

# Make a change
echo "Hello from feature branch" > demo.txt
git add demo.txt
git commit -m "feat: add demo.txt file"
```

---

## 2️⃣ Push the branch to GitHub

```bash
git push -u origin feature/demo
```

You could open a PR on GitHub, **or** merge locally.

---

## 3️⃣ Merge into main locally

```bash
git switch main
git pull origin main          # make sure main is updated
git merge feature/demo        # merge commit will be created if needed
```

* If there’s no conflict, Git auto-merges.
* If there’s a conflict, Git will pause and ask you to resolve files, then:

```bash
git add <resolved-files>
git commit
```

---

## 4️⃣ Push the merged main branch Github

```bash
git push origin main
```

---

## 5️⃣ (Optional) Delete the feature branch after merge

```bash
git branch -d feature/demo            # delete local
git push origin --delete feature/demo # delete remote
```

---

