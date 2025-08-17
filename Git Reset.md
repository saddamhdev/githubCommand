What is git reset?

Great question 👍 `git reset` is one of the most **powerful but dangerous** Git commands because it can change history.

---

## 🔹 What is `git reset`?

`git reset` moves the **current branch pointer (like `main`)** and optionally your **working directory** and **staging area** (index) to a different commit.

👉 In simple words:

* It tells Git: **“Go back to this commit, and forget the commits after it (depending on mode).”**

---

## 🔹 Three main modes of `git reset`

### 1. **Soft reset (`--soft`)**

```bash
git reset --soft <commit>
```

* Moves branch pointer to `<commit>`.
* Keeps changes staged (in index).
* Useful if you want to “redo” commits but keep the changes ready to recommit.

Example:

```
A -- B -- C (HEAD -> main)
```

`git reset --soft B`

```
A -- B (HEAD -> main)
       \
        C (changes staged)
```

---

### 2. **Mixed reset (`--mixed`)** (default)

```bash
git reset --mixed <commit>
git reset <commit>   # same thing
```

* Moves branch pointer to `<commit>`.
* Keeps changes in **working directory**, but **unstaged**.
* Useful if you want to uncommit changes but not lose them.

---

### 3. **Hard reset (`--hard`)**

```bash
git reset --hard <commit>
```

* Moves branch pointer to `<commit>`.
* **Deletes** all changes in staging and working directory.
* ⚠️ Dangerous: you lose everything after `<commit>` (unless you recover via `git reflog`).

---

## 🔹 Example

Say history is:

```
A -- B -- C -- D (HEAD -> main)
```

### `git reset --soft B`

* Branch moves back to B.
* Commits C and D disappear, but their changes are staged.

### `git reset --mixed B`

* Branch moves back to B.
* Commits C and D disappear, but their changes are unstaged in working directory.

### `git reset --hard B`

* Branch moves back to B.
* Commits C and D disappear, and changes are **gone** from working directory too.

---

## 🔹 When do you use `git reset`?

1. Undo commits (fix mistakes in local history).
2. Move HEAD/branch pointer backward.
3. Clean up commits before pushing to remote.

---

✅ **Summary:**

* `--soft` → keep changes staged.
* `--mixed` (default) → keep changes unstaged.
* `--hard` → erase everything after commit.

---

👉 Do you want me to also compare `git reset` vs `git revert` (since both “undo commits” but behave very differently)?

