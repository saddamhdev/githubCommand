Ah! **Git stash** is a super handy command to **temporarily save your changes** without committing them. Let’s break it down clearly.

---

## 🔹 What is Git Stash?

* Sometimes you’re working on something but need to **switch branches** or **pull updates**, and you **don’t want to commit incomplete changes**.
* `git stash` **saves your working directory and staging area temporarily** and **clears your working directory**.
* Later, you can **restore those changes**.

---

## 🔹 Basic Commands

### 1. Stash your changes

```bash
git stash
```

* Saves all **unstaged and staged changes**.
* Working directory becomes **clean**.

Optionally, add a message:

```bash
git stash save "WIP: login feature"
```

---

### 2. List stashed changes

```bash
git stash list
```

Example output:

```
stash@{0}: WIP on main: 123abc4 WIP: login feature
stash@{1}: WIP on main: 789def0
```

---

### 3. Apply stashed changes

```bash
git stash apply
```

* Applies the **latest stash** but keeps it in the stash list.

Apply a specific stash:

```bash
git stash apply stash@{1}
```

---

### 4. Pop stash

```bash
git stash pop
```

* Applies the **latest stash** and **removes it** from the stash list.

---

### 5. Drop a stash

```bash
git stash drop stash@{0}
```

* Deletes a stash from the list.

---

### 6. Clear all stashes

```bash
git stash clear
```

* Deletes **all stashes**.

---

## 🔹 Example Workflow

```bash
# You modify files but cannot commit yet
git status

# Save changes temporarily
git stash save "WIP: new feature"

# Switch branch
git checkout main
git pull

# Return to your work
git checkout feature
git stash pop
```

* Now your changes are restored, ready to continue working.

---

💡 **Tip:**

* Stash is useful when you want a **clean working directory quickly**.
* You can stash **untracked files** using:

```bash
git stash -u
```

---

If you want, I can make a **visual diagram showing stash, pop, apply, and stash list** — it makes it super easy to understand.

Do you want me to do that?



How one more stash create


Creating **more than one stash** in Git is easy — Git keeps a **stack of stashes**, so you can stash multiple sets of changes.

---

## 🔹 Steps to Create Multiple Stashes

### 1. Make some changes and stash

```bash
# Modify some files
git stash save "WIP: first feature"
```

### 2. Make more changes and stash again

```bash
# Modify other files
git stash save "WIP: second feature"
```

---

### 3. Check all stashes

```bash
git stash list
```

Example output:

```
stash@{0}: WIP: second feature
stash@{1}: WIP: first feature
```

* `stash@{0}` → most recent
* `stash@{1}` → older

---

### 4. Apply or pop a specific stash

```bash
# Apply without removing
git stash apply stash@{1}

# Apply and remove
git stash pop stash@{0}
```

---

### 🔹 Notes

* Each `git stash` creates a **new entry in the stash stack**.
* You can create **as many stashes as needed**.
* Use **descriptive messages** to remember which stash is which.

---

💡 **Tip:**

* `git stash show -p stash@{n}` → see the changes inside a specific stash.

---

If you want, I can make a **diagram showing multiple stashes being created and applied**, which makes it much easier to visualize.

Do you want me to do that?




