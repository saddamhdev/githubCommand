**Awesome—here’s **HEAD (Git & GitHub) explained from Beginner → Senior**, with the exact commands you’ll use at each level.

# Beginner: Mental model + must-know commands

## What is HEAD (Git)?

* **HEAD = “where you are now.”** It points to the commit your working tree is based on.
* Usually it points to the **tip of your current branch**.

### See it

```bash
git status                          # shows current branch
git rev-parse --abbrev-ref HEAD     # prints branch name or 'HEAD' if detached
git log --oneline --decorate -5     # shows HEAD → branch → commit
```

### Move it (safely)

```bash
git switch main                     # move to branch 'main'
git switch -c feature/x             # new branch from here
git restore --staged .              # unstage files
git restore .                       # discard local changes (careful)
```

## What is “HEAD” on GitHub?

* In URLs, `HEAD` means “**default branch tip**” (often `main`). Links won’t break if default changes.

  ```
  https://github.com/OWNER/REPO/blob/HEAD/path/to/file
  ```
* In Pull Requests:

  * **head** = source branch of the PR
  * **base** = target branch to merge into

---

# Intermediate: Detached HEAD, undo, recovery, PR refs

## Detached HEAD (what & why)

* Happens when you checkout a commit instead of a branch:

```bash
git switch --detach <commit|HEAD~1>
```

* You can test or build from old commits. If you commit here, **save it**:

```bash
git switch -c fix/from-old         # turns detached work into a branch
```

## Undo correctly (choose the right tool)

* **Undo last commit, keep changes staged**:

```bash
git reset --soft HEAD~1
```

* **Undo last commit, unstage but keep files**:

```bash
git reset --mixed HEAD~1           # default reset mode
```

* **Hard reset (dangerous: discards changes)**:

```bash
git reset --hard HEAD~1
```

* **Public history? Prefer revert**:

```bash
git revert <sha>                   # adds a new commit that undoes
```

## Lifesaver: Reflog (HEAD’s diary)

```bash
git reflog                         # every HEAD move
git checkout HEAD@{2}              # jump to where HEAD was 2 moves ago
```

## Compare local vs remote

```bash
git fetch origin
git log --oneline --decorate --graph HEAD..origin/main   # what you’re behind
git diff origin/main...HEAD                              # what you changed
```

## GitHub PR refs (work without adding the fork)

```bash
git fetch origin pull/123/head:pr-123       # PR source branch tip
git fetch origin pull/123/merge:pr-123-merge# GitHub’s test-merge result
```

## Handy notations

* `HEAD~N` (N ancestors), `HEAD^` (parent), `@` ≡ `HEAD`
* Range selection:

```bash
git log A..B      # commits reachable from B not from A
git diff A...B    # diff between merge bases and B
```

---

# Senior: Internals, refspecs, CI, and advanced workflows

## Refs & symrefs

* `.git/HEAD` usually contains:

  ```
  ref: refs/heads/main
  ```

  That’s a **symbolic ref** → points to a ref which points to a commit.
* Detached state: `.git/HEAD` holds a **raw SHA** (no `ref:` line).
* Branch tips live in `.git/refs/heads/*` or in `packed-refs`.

## Remote HEAD & default branch detection

```bash
git ls-remote --symref origin HEAD
# refs/heads/main    HEAD
# <sha>              refs/heads/main
```

This tells you the server’s default branch.

## Refspecs (fetch/push control)

```bash
# Fetch only main and a PR head
git fetch origin refs/heads/main:refs/remotes/origin/main \
                 refs/pull/123/head:refs/remotes/origin/pr-123
```

## CI/CD (GitHub Actions) essentials

```yaml
steps:
  - uses: actions/checkout@v4   # checks out GITHUB_SHA
  - run: |
      echo "SHA=$GITHUB_SHA"
      echo "REF=$GITHUB_REF"            # refs/heads/main or refs/pull/123/merge
      echo "HEAD_REF=${{ github.head_ref }}"  # PR source
      echo "BASE_REF=${{ github.base_ref }}"  # PR target
```

## History surgery (with team safety)

* **Interactive rebase** to clean local series:

```bash
git rebase -i origin/main
```

* **Split a commit**:

```bash
git rebase -i <base>  # mark commit as 'edit'
# make changes
git commit --amend
git rebase --continue
```

* **Move a feature onto new base**:

```bash
git fetch origin
git rebase origin/main feature/x
```

* **When rewriting shared history**: coordinate, force-push once, and post migration notes:

```bash
git push --force-with-lease
```

## Forensics & recovery

* Find the merge base for precise diffs:

```bash
git merge-base main feature/x
```

* Recover a “lost” branch:

```bash
git reflog | grep <branch-or-message>
git branch recovered <sha>
```

## Binary search bugs

```bash
git bisect start
git bisect bad                          # current is bad
git bisect good <known-good-sha>
# test each checkout → mark good/bad until culprit appears
git bisect reset
```

---

# Quick checklists by level

**Beginner should:**

* Explain HEAD, branch tips, detached HEAD.
* Safely switch branches; create branches.
* Use `status`, `log --decorate`, `rev-parse --abbrev-ref HEAD`.

**Intermediate should:**

* Recover with reflog; choose reset vs revert.
* Work from detached HEAD then branch it.
* Compare local vs remote; fetch PR refs.

**Senior should:**

* Read/interpret `.git/HEAD`, `packed-refs`, and symrefs.
* Use refspecs and CI variables; automate PR fetch/merge testing.
* Perform safe history rewrites; guide team process and recovery.

---

If you want, I can generate a **one-file demo script** you can paste in a temp folder that creates commits (A/B/C), shows detached HEAD, recovers with reflog, and fetches a PR ref—so you can watch HEAD move step by step.
**
