Ah, **`git restore`** is a newer Git command (introduced in Git 2.23) that helps you **undo changes** in a safer and more intuitive way than `checkout` for files.

---

## 🔹 What `git restore` Does

`git restore` can:

1. **Discard changes in your working directory** (unstaged changes).
2. **Unstage files** from the staging area (like `git reset HEAD <file>`).

It **does not affect commits** unless combined with `--source`.

---

## 🔹 Common Usage

### 1. Discard unstaged changes (working directory)

Suppose you modified `file.txt` but haven’t staged it yet:

```bash
git restore file.txt
```

* Restores `file.txt` to **last committed state**.
* Any unsaved changes in the file are lost.

---

### 2. Unstage a staged file

If you ran `git add file.txt` but want to unstage it:

```bash
git restore --staged file.txt
```

* Removes the file from the staging area.
* Your **working directory changes remain**.

---

### 3. Restore a file from a specific commit

```bash
git restore --source <commit_hash> file.txt
```

* Replaces the file in your working directory with the version from `<commit_hash>`.
* Useful if you want to **go back to a previous version of a file**.

---

### 4. Restore all files

Discard **all unstaged changes** in the repo:

```bash
git restore .
```

---

## 🔹 Difference from `git checkout`

* `git checkout <file>` used to do all of this, but it’s **less clear**.
* Git introduced `git restore` (for files) and `git switch` (for branches) to **separate responsibilities**.

---

### 🔹 Quick Summary Table

| Action                            | Command                                |
| --------------------------------- | -------------------------------------- |
| Discard working directory changes | `git restore <file>`                   |
| Unstage a file                    | `git restore --staged <file>`          |
| Restore from previous commit      | `git restore --source <commit> <file>` |
| Discard all changes               | `git restore .`                        |

---

💡 **Tip:** Always double-check with `git status` before restoring — once you restore, unsaved changes are **lost**.

---

If you want, I can make a **visual diagram showing how `git restore` affects staging vs working directory** — it makes it very easy to understand.

Do you want me to do that?
