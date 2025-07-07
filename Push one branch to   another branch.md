<project>

 
    i have download project from github. and some coded. now i want to upload updated code from abdukbari branch

</project>

<details>
  <summary><strong>Self branch To Push </strong> </summary>
  To upload (push) your updated code to the `abdulbari` branch on GitHub, follow these steps:

---

### ✅ Prerequisites

Ensure you have:

* Git installed
* Access to the GitHub repository
* Proper authentication (token or SSH key)

---

### 🔁 Step-by-Step Instructions

#### 1. **Open Terminal / Git Bash** in your project folder

```bash
cd path/to/your/project
```

---

#### 2. **Check the current branch**

```bash
git branch
```

If you're not already on the `abdulbari` branch:

```bash
git checkout abdulbari
```

If the branch doesn't exist locally:

```bash
git checkout -b abdulbari origin/abdulbari
```

---

#### 3. **Add your changes**

```bash
git add .
```

Or add specific files:

```bash
git add filename1 filename2
```

---

#### 4. **Commit your changes**

```bash
git commit -m "Your commit message describing the changes"
```

---

#### 5. **Push to GitHub**

```bash
git push origin abdulbari
```

---

### 🔐 If using HTTPS and you're asked for credentials

You may need to use a **GitHub Personal Access Token** instead of your password. Create one [here](https://github.com/settings/tokens) if you haven't already.

---

### ✅ To confirm it worked

Visit your GitHub repo and check the **`abdulbari`** branch. Your changes should be there.

---

Let me know if you run into any error (e.g., authentication, permission, merge conflicts), and I’ll help you fix it!

</details>

<details>
  <summary><strong>Other branch To Push </strong> </summary>
  Yes, absolutely — you **can push your changes to the `fuad` branch** if:

1. ✅ The branch exists on the remote (GitHub or other).
2. ✅ You have permission to push.

---

### 🧾 Steps to Push to `fuad` Branch

#### 1. Make sure you're on the `fuad` branch:

```bash
git branch
```

If you're already on `fuad`, you're good.

---

#### 2. Add and Commit your changes:

```bash
git add .
git commit -m "Your meaningful commit message"
```

---

#### 3. Push to remote `fuad` branch:

```bash
git push origin fuad
```

---

### 🔎 How to Check if `fuad` Exists on Remote?

You can list remote branches:

```bash
git branch -r
```

If you see `origin/fuad`, it exists on the remote.

---

### 🚨 First-time push? (If remote doesn’t have `fuad` yet)

Then push like this to create it remotely:

```bash
git push -u origin fuad
```

---

Let me know if you face an error while pushing — I can help fix it quickly!

</details>

