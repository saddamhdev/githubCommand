অসাধারণ প্রশ্ন 👍
হ্যাঁ, **একটা লোকাল branch একসাথে একটাই remote branch কে track করতে পারে** (default tracking branch)।
কিন্তু আপনি চাইলে **একই project এ একাধিক remote** রাখতে পারেন, আর ভিন্ন ভিন্ন লোকাল branch কে আলাদা remote branch track করাতে পারেন।

---

## 🔹 ১) নতুন Remote যোগ করা

```bash
git remote add upstream https://github.com/ORIGINAL/PROJECT.git
```

👉 এখন আপনার কাছে দুইটা remote হলো:

* `origin` → আপনার fork
* `upstream` → মূল project

দেখতে চাইলে:

```bash
git remote -v
```

---

## 🔹 ২) লোকাল ব্রাঞ্চ তৈরি + tracking সেট করা

```bash
git checkout -b feature_x upstream/main
```

👉 এর মানে:

* নতুন লোকাল branch `feature_x` বানালো
* যেটা track করছে `upstream/main` কে

---

## 🔹 ৩) Existing branch কে অন্য branch track করানো

```bash
git branch --set-upstream-to=origin/dev dev
```

👉 এখন লোকাল `dev` branch track করবে `origin/dev` কে।

---

## 🔹 ৪) Tracking status দেখা

```bash
git branch -vv
```

Output এরকম আসবে:

```
* main     123abc [origin/main] Some commit msg
  dev      456def [origin/dev]  Work in progress
  feature  789ghi [upstream/main] Testing branch
```

👉 এখানে স্পষ্ট বোঝা যায় কোন লোকাল branch কোন remote branch কে track করছে।

---

## 🔹 Summary

* **একটা লোকাল branch = একটাই tracking remote branch**
* কিন্তু আপনি **একই repo তে multiple remote রাখতে পারেন**
* আর **প্রতিটি লোকাল branch কে ভিন্ন remote branch track করাতে পারেন**

---

💡 টিমে কাজ করলে সাধারণত:

* `origin` = নিজের fork
* `upstream` = মূল project repo
  লোকাল `main` → track করে `upstream/main`
  লোকাল `my-feature` → push হয় `origin/my-feature`

---




👌 খুব ভালো করেছেন — এখন আসল সমস্যাটা হলো আপনার **upstream repo তে `main` নেই, ওখানে ব্রাঞ্চের নাম `master`**।

---

### 🔹 কেন error হলো?

আপনি যখন চালালেন

```bash
git checkout -b feature_x upstream/main
```

Git বললো:

```
fatal: 'upstream/main' is not a commit
```

কারণ upstream এ **main branch নাই**, ওখানে আছে `master`।

---

### 🔹 কিভাবে ঠিক করবেন?

1. আগে fetch করে নিন upstream এর সব branch:

```bash
git fetch upstream
```

2. এখন upstream এর branch গুলো দেখতে:

```bash
git branch -r
```

Output এরকম হবে:

```
origin/main
upstream/master
```

3. এখন নতুন branch বানান upstream/master থেকে:

```bash
git checkout -b feature_x upstream/master
```

👉 এতে আপনার লোকাল branch `feature_x` তৈরি হবে যেটা track করবে `upstream/master` কে।

---

### 🔹 Important Note

* আপনার **origin repo** (GitHub fork) এ branch নাম → `main`
* আপনার **upstream repo** এ branch নাম → `master`

তাই দুটো আলাদা আলাদা।

---


বুঝলাম 👍 আপনি upstream যোগ করেছেন, fetch ও করেছেন, কিন্তু এখনো **লোকালে upstream branch checkout করেননি**। এজন্য আপনার working directory তে upstream এর কোড দেখা যাচ্ছে না।

চলুন step by step করে নিই 👇

---

## 🔹 Step 1: নিশ্চিত করুন upstream branch এসেছে

```bash
git fetch upstream
git branch -r
```

👉 এখানে লিস্টে `upstream/master` দেখতে পাবেন।

---

## 🔹 Step 2: লোকালে নতুন branch বানান (upstream থেকে)

```bash
git checkout -b upstream-master upstream/master
```

👉 এখন আপনার লোকালে একটা নতুন branch হবে `upstream-master`, যেটা track করবে upstream এর master কে।

---

## 🔹 Step 3: কোড দেখা

এখন আপনি লোকাল `upstream-master` branch এ থাকবেন → এখানে upstream repo এর কোড দেখা যাবে।

---

## 🔹 Step 4 (optional): main এর সাথে মেশাতে চাইলে

যদি চান upstream এর code আপনার লোকাল main এ নিয়ে আসতে:

```bash
git switch main
git merge upstream/master
```

অথবা clean history চান →

```bash
git switch main
git rebase upstream/master
```

---

## ✅ Summary

* শুধু `git remote add` করলে code আসে না
* শুধু `git fetch upstream` করলে code আসে `.git` এর ভেতরে, কিন্তু checkout না করলে দেখা যায় না
* `git checkout -b newbranch upstream/master` করলে তখন লোকালে দেখা যাবে

---





