Got it — **“restore branch”** usually means you deleted or lost a branch pointer and want it back. You don’t use `git restore` for that (it’s for files). Use **`git branch` / `git switch` + reflog**.

### Quick cases

**1) The branch still exists on remote**

```bash
git fetch origin
git switch -c <branch> --track origin/<branch>
# older: git checkout -b <branch> origin/<branch>
```

**2) You deleted a local branch; recreate it from its last commit via reflog**

```bash
git reflog                 # find the last commit sha for that branch tip
git switch -c <branch> <sha>
# or: git branch <branch> <sha>
```

**3) Remote branch was deleted; recover from remote-tracking reflog (if available)**

```bash
git reflog show refs/remotes/origin/<branch>   # find last sha
git branch <branch> <sha>
git push -u origin <branch>                    # republish to remote
```

**4) You moved the branch head by mistake (e.g., bad reset) and want the previous state**

```bash
git reflog                         # find the previous HEAD, e.g., HEAD@{1}
git reset --hard HEAD@{1}          # moves current branch back (DANGEROUS: discards WD/Index)
# safer, just bring files back without moving history:
# git restore --staged --worktree --source=HEAD@{1} .
```

### Tips

* `git log --oneline --all --grep "<message part>"` can help find the commit if you remember the message.
* If you committed while in a detached HEAD, recover with:
  `git reflog` → get that commit → `git branch <branch> <sha>`.

If you tell me what exactly happened (deleted locally? reset? remote gone?), I’ll give you the exact two or three commands to run.
