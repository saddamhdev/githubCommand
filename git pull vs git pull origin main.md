চমৎকার প্রশ্ন 🙂 অনেকে `git pull` আর `git pull origin main` গুলিয়ে ফেলে। আসল পার্থক্যটা হলো **default tracking branch** বনাম **explicit remote + branch** উল্লেখ করা।

---

## 🔹 ১) `git pull`

👉 শুধু `git pull` লিখলে Git আপনার **current branch** যেটার সাথে রিমোটে tracking set করা আছে, সেটাকে update করবে।

* যদি আপনি `main` branch-এ থাকেন
* আর লোকাল `main` already track করে `origin/main` কে
  তাহলে `git pull` মানে হবে:

```
git pull origin main
```

💡 **Shortcut:** এটা কাজ করে কারণ লোকাল branch-এর সাথে রিমোট branch লিঙ্ক করা থাকে।

---

## 🔹 ২) `git pull origin main`

👉 এখানে আপনি স্পষ্ট করে বলছেন:

* কোন রিমোট (origin) থেকে
* কোন ব্রাঞ্চ (main) কে
  পুল করতে হবে।

এটা **safe এবং exact** command, confusion কম।

---

## 🔹 Example

ধরুন আপনার লোকালে দুইটা রিমোট আছে:

* `origin` → GitHub
* `upstream` → মূল project repo

তখন শুধু `git pull` দিলে Git **origin** ধরবে (default remote)।
কিন্তু আপনি যদি `upstream/main` থেকে আপডেট চান, তখন লিখতে হবে:

```bash
git pull upstream main
```

---

## 🔹 তুলনা টেবিলে

| Command                | কী করে?                                                                                              |
| ---------------------- | ---------------------------------------------------------------------------------------------------- |
| `git pull`             | বর্তমান branch যেটাকে track করছে, সেই রিমোট branch থেকে আপডেট আনে (default tracking branch অনুযায়ী)। |
| `git pull origin main` | স্পষ্ট করে বলে দেয় → “origin” রিমোটের “main” branch থেকে আপডেট আনো।                                  |

---

## 🔹 Best Practice

* একা কাজ করলে `git pull` যথেষ্ট।
* কিন্তু টিমে একাধিক রিমোট বা একাধিক tracking থাকলে → সবসময় `git pull origin main` ব্যবহার করা ভালো।

---





have one more tracking remote brach? how create

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




