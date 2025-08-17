Here’s what those flags mean (with the common commands they’re used with):

* **`-d`** — **Delete a branch (safe)**.
  Used with `git branch`: deletes a local branch only if it’s already merged.
  Example: `git branch -d feature/ui`. (Force delete is `-D`.) ([git-scm.com][1])

* **`-u`** — **Set upstream (tracking) branch**.
  Used with `git branch` to set tracking for the current (or named) branch:
  `git branch -u origin/feature/ui`
  Also used with `git push -u origin <branch>` to push and set upstream in one go. ([git-scm.com][1])

* **`-c`** — **Create** in two contexts:

  1. With **`git switch -c <new>`** → create **and switch** to a new branch. ([git-scm.com][2])
  2. With **`git branch -c <old> <new>`** → **copy** an existing branch (config + reflog) to a new name (different from rename). ([git-scm.com][1])

* **`-b`** — **Create (and switch) a new branch**.
  Used with `git checkout -b <new> [start-point]` → creates the branch and checks it out. Modern equivalent is `git switch -c <new>`. ([git-scm.com][3])

Quick tips:

* Delete **remote** branches with: `git push origin --delete <branch>`.
* Prefer `git switch -c` for new branches and `git switch <name>` for switching; keep `git checkout -b` in mind for older Git. ([git-scm.com][2])

Want a tiny cheat sheet image or a one-line alias setup (e.g., `gbd` for delete)?

[1]: https://git-scm.com/docs/git-branch "Git - git-branch Documentation"
[2]: https://git-scm.com/docs/git-switch?utm_source=chatgpt.com "Git - git-switch Documentation"
[3]: https://git-scm.com/docs/git-checkout "Git - git-checkout Documentation"
