Here’s a clean cheat-sheet for `git branch` 👇

### What it does

`git branch` **manages branches** (lightweight pointers to commits). It **doesn’t switch** your working directory—that’s `git switch`/`git checkout`.

---

### List & inspect

```bash
git branch                 # list local branches (current is starred *)
git branch -r              # list remote-tracking branches
git branch -a              # list all (local + remote)
git branch -vv             # show each branch’s last commit + upstream
git branch --show-current  # print current branch name
git branch --contains <sha>    # which branches contain a commit
git branch --merged            # branches already merged into current
git branch --no-merged         # branches not yet merged
```

### Create

```bash
git branch feature/login           # create at current HEAD
git branch feature/api <commit>    # create at specific commit
# create AND switch (recommended):
git switch -c feature/ui           # same as: git checkout -b feature/ui
```

### Switch (not strictly `git branch`, but related)

```bash
git switch main            # switch branches (newer command)
git checkout main          # older, still works
```

### Rename

```bash
git branch -m old-name new-name   # rename any branch (not checked out)
git branch -m new-name            # rename current branch
```

### Delete

```bash
git branch -d feature/ui     # safe delete (only if merged)
git branch -D feature/ui     # force delete (even if unmerged) ⚠️
# delete remote branch:
git push origin --delete feature/ui
```

### Track upstream / publish

```bash
git push -u origin feature/ui          # push new branch & set upstream
git branch -u origin/feature/ui        # set upstream for current branch
git branch -vv                         # verify tracking
```

### Remote cleanup

```bash
git fetch --prune            # remove stale remote-tracking refs
git remote prune origin      # deeper prune of stale refs
```

### Default branch name for new repos

```bash
git config --global init.defaultBranch main
```

---

#### Typical workflow

```bash
git switch -c feature/payment
# ... do work ...
git push -u origin feature/payment
# open PR, merge...
git switch main
git pull
git branch -d feature/payment        # local cleanup
git push origin --delete feature/payment   # remote cleanup
```

Want a tiny demo script (like before) that you can copy-paste to see this end-to-end in a fresh repo? I can drop one in a single block.
