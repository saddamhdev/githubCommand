চমৎকার, এবার আসি 👉 **`git pull`**

---

## 🔹 `git pull` কী করে?

👉 **`git pull` = `git fetch` + `git merge` (by default)**

মানে:

1. প্রথমে রিমোট থেকে নতুন commit গুলো লোকালে নামায় (fetch করে)
2. তারপর আপনার current branch-এর সাথে সেই commit গুলো merge করে দেয়

---

## 🔹 Example Scenario

### রিমোটে (GitHub এ) main branch:

```
A---B---C   (origin/main)
```

### আপনার লোকালে:

```
A---B       (main)
```

---

### Step 1: `git pull origin main`

1. Git fetch করবে → origin/main এখন `A---B---C`
2. Git merge করবে → লোকাল main = `A---B---C`

---

## 🔹 Visual (Behind → Updated)

```
Before pull:                 After pull:
main:        A---B           main:        A---B---C
origin/main: A---B---C       origin/main: A---B---C
```

---

## 🔹 Special Cases

### 1) Fast-forward merge (সবচেয়ে common)

👉 যদি আপনার লোকাল main এ কোনো নতুন commit না থাকে
তাহলে সরাসরি রিমোটের commit যোগ হয়ে যাবে (fast-forward)।

---

### 2) Merge commit তৈরি হবে

👉 যদি আপনার লোকালেও নতুন commit থাকে আর রিমোটেও নতুন commit থাকে
তাহলে git একটা **merge commit** বানাবে।

```
     C (origin/main)
    /
A---B
    \
     D (main)
```

`git pull` করলে merge commit তৈরি হবে:

```
     C
    / \
A---B---M (merge)
    \
     D
```

---

### 3) Rebase mode

কিছু টিমে policy থাকে **merge commit এড়াতে**। তখন `git pull --rebase` ব্যবহার হয়:

```bash
git pull --rebase origin main
```

👉 এতে আপনার লোকাল commit গুলো রিমোট commit এর উপরে বসে যায় (history পরিষ্কার থাকে)।

---

## 🔹 Summary

* `git fetch` → শুধু ডাটা আনে (main আপডেট করে না)
* `git merge` → origin/main এর সাথে লোকাল main merge করে
* `git pull` = fetch + merge (দুটো একসাথে করে)
* `git pull --rebase` = fetch + rebase

---

💡 Teamwork এ প্রতিদিন code শুরু করার আগে 👉 `git pull` main branch এ করা best practice।

---

আপনি কি চান আমি **git fetch vs git pull এর side-by-side তুলনা একটা টেবিল/ডায়াগ্রামে** দেখাই?
