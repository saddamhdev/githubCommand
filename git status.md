আচ্ছা ভাই 🙂 এখন দেখি `git status` কীভাবে কাজ করে।

---

## 🔹 `git status` কী করে?

* আপনার **working directory**, **staging area (index)**, আর **current branch** এর অবস্থা দেখায়।
* সহজ ভাষায়: *"আমি কোন branch এ আছি, আমার কোডে কী কী পরিবর্তন হয়েছে, push/pull বাকি আছে কিনা।"*

---

## 🔹 Output Sections

### 1) Branch info

```bash
On branch main
Your branch is up to date with 'origin/main'.
```

👉 জানায় আপনি কোন branch এ আছেন আর সেটা রিমোটের সাথে sync আছে কিনা।

---

### 2) Working directory changes

```bash
Changes not staged for commit:
  modified:   file1.txt
```

👉 মানে file change করেছেন কিন্তু `git add` করেননি।

---

### 3) Staging area changes

```bash
Changes to be committed:
  new file:   file2.txt
```

👉 মানে `git add` করেছেন, এখন শুধু `git commit` করা বাকি।

---

### 4) Untracked files

```bash
Untracked files:
  newfile.txt
```

👉 মানে নতুন ফাইল বানিয়েছেন কিন্তু এখনো Git এর ট্র্যাকিং এ আনেননি।

---

### 5) Remote tracking info

```bash
Your branch is ahead of 'origin/main' by 2 commits.
```

👉 মানে আপনার লোকাল এ ২টা কমিট আছে, যেগুলো এখনো push হয়নি।

```bash
Your branch is behind 'origin/main' by 1 commit.
```

👉 মানে রিমোটে ১টা কমিট আছে, যেটা আপনাকে pull করতে হবে।

---

## 🔹 Quick Example

ধরুন আপনি লোকালে কিছু কোড লিখলেন:

```bash
echo "Hello" > hello.txt
```

এখন চালান:

```bash
git status
```

Output হবে:

```
On branch main
Untracked files:
  hello.txt
```

তারপর `git add hello.txt` দিলে:

```
Changes to be committed:
  new file:   hello.txt
```

---

✅ **সংক্ষেপে**

* `git status` = বর্তমান branch + পরিবর্তিত ফাইলের অবস্থা + push/pull needed info
* Git শেখার সময় এটা সবচেয়ে বেশি ব্যবহার হয়

---







দারুণ 🙂 আমি আপনার জন্য **`git fetch origin` এর পর git status Cheat Sheet** বাংলায় বানালাম।
এখন যেকোনো টিম প্রোজেক্টে দেখলেই বুঝবেন অবস্থা কী 👇

---

# 📌 Git Status Cheat Sheet (After `git fetch origin`)

### ✅ 1) লোকাল আপ টু ডেট

```
On branch main
Your branch is up to date with 'origin/main'.
```

👉 মানে আপনার লোকাল `main` আর রিমোট `main` একই জায়গায় আছে, কিছু করার দরকার নেই।

---

### ⬇️ 2) লোকাল পিছিয়ে আছে (behind)

```
On branch main
Your branch is behind 'origin/main' by 2 commits, and can be fast-forwarded.
  (use "git pull" to update your local branch)
```

👉 মানে রিমোটে ২টা নতুন commit আছে → আপনাকে `git pull` করতে হবে।

---

### ⬆️ 3) লোকাল এগিয়ে আছে (ahead)

```
On branch main
Your branch is ahead of 'origin/main' by 1 commit.
  (use "git push" to publish your local commits)
```

👉 মানে আপনার লোকালে ১টা commit আছে → যেটা এখনো push হয়নি।

---

### 🔀 4) লোকাল আর রিমোট দুইদিকে আলাদা (diverged)

```
On branch main
Your branch and 'origin/main' have diverged,
and have 1 and 2 different commits each, respectively.
  (use "git pull" to merge the remote branch into yours)
```

👉 মানে:

* আপনার লোকালে extra commit আছে
* রিমোটেও extra commit আছে
* এখন merge বা rebase করে দুটো মেলাতে হবে

---

### 📄 5) Untracked / Staged / Modified files

এগুলো fetch-এর সাথে সরাসরি সম্পর্কিত না, বরং আপনার working directory এর অবস্থা:

* `Untracked files:` → নতুন ফাইল যেটা git add করেননি
* `Changes to be committed:` → staging area-তে add করা আছে
* `Changes not staged for commit:` → পরিবর্তন করেছেন কিন্তু add করেননি

---

## 🔹 Workflow (Best Practice)

প্রতিদিন টিমে কাজ শুরু করার আগে:

```bash
git fetch origin
git status
```

👉 এরপর status অনুযায়ী action নিন:

* **behind** → `git pull`
* **ahead** → `git push`
* **diverged** → `git pull --rebase` বা `merge` (team policy)

---

📌 এখন প্রশ্ন: আপনি কি চান আমি এটাকে একটা সুন্দর **PDF checklist** বানিয়ে দিই যাতে আপনার কাছে সবসময় রেফারেন্স থাকে?
