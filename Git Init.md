`git init` হলো Git-এর একদম প্রথম কমান্ডগুলোর একটি।
এটা ব্যবহার করে আপনি **নতুন একটা Git repository** তৈরি করেন।

---

## 🔹 কাজ কী করে?

```bash
git init
```

* আপনার বর্তমান ডিরেক্টরির ভেতর `.git` নামের একটি **লুকানো ফোল্ডার** তৈরি করে।
* এই `.git` ফোল্ডারেই আপনার প্রজেক্টের **সমস্ত version history, branches, commits** ইত্যাদি সংরক্ষণ হয়।
* এরপর থেকে সেই ফোল্ডারের ভেতরে Git কমান্ড ব্যবহার করে version control করতে পারবেন।

---

## 🔹 ব্যবহার উদাহরণ

### 1. নতুন রিপোজিটরি শুরু করা

```bash
mkdir my-project
cd my-project
git init
```

👉 এখন `my-project` ফোল্ডারটি একটি Git repository হয়ে গেল।

---

### 2. ফাইল যোগ করে কমিট করা

```bash
echo "Hello Git" > file.txt
git add file.txt
git commit -m "First commit"
```

👉 এতে প্রথম কমিট তৈরি হলো।

---

### 3. রিমোট রিপোজিটরি যুক্ত করা

লোকাল রিপোকে GitHub/GitLab ইত্যাদির সাথে লিঙ্ক করতে:

```bash
git remote add origin https://github.com/user/my-project.git
git push -u origin main
```

---

## 🔹 কখন ব্যবহার করবেন?

* যখন **একদম নতুন প্রজেক্ট** শুরু করছেন।
* যখন কোনো **ফোল্ডারকে Git দিয়ে ট্র্যাক** করতে চান।
* যখন আপনি **নিজের লোকাল repository তৈরি করে পরে রিমোটে পুশ** করবেন।

---

⚠️ নোট: যদি আপনি আগে থেকেই GitHub থেকে কোনো রিপো **clone** করেন (`git clone`), তখন `git init` দেওয়ার দরকার নেই, কারণ `.git` ফোল্ডার আগে থেকেই থাকে।

---

👉 চাইলে আমি তোমাকে **`git init` বনাম `git clone`** এর পার্থক্যও বুঝিয়ে দিতে পারি। সেটা কি দেখাব?
