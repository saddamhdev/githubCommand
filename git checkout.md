ঠিক আছে 🙂 এখন চলুন **`git checkout`** পুরোটা ব্যাখ্যা করি।

---

# 🔹 `git checkout` কী?

👉 **`git checkout`** হলো Git এর একটা কমান্ড, যেটা ব্যবহার করে আপনি –

1. অন্য কোনো **branch** এ যেতে পারেন,
2. অথবা কোনো নির্দিষ্ট **commit / file version** দেখতে বা restore করতে পারেন।

---

# 🔹 ব্যবহার ১: Branch switch করা

```bash
git checkout branch-name
```

👉 এখানে আপনি `main` থেকে `feature-x` এ চলে গেলেন।

Example:

```bash
git checkout main
```

→ এখন আপনার working directory `main` branch এর কোডে চলে যাবে।

---

# 🔹 ব্যবহার ২: নতুন branch তৈরি + switch

```bash
git checkout -b new-feature
```

👉 এটা দুইটা কাজ একসাথে করে:

* নতুন branch বানাবে → `new-feature`
* ওই branch এ switch করবে

---

# 🔹 ব্যবহার ৩: পুরনো commit দেখা (detached HEAD state)

```bash
git checkout <commit-hash>
```

👉 আপনি তখন ওই commit এর snapshot দেখতে পাবেন, কিন্তু branch এ থাকবেন না।

Example:

```bash
git checkout a1b2c3d
```

→ এখন আপনার HEAD ওই commit এ গেছে।

---

# 🔹 ব্যবহার ৪: নির্দিষ্ট file restore করা

```bash
git checkout main -- filename.txt
```

👉 এখানে `filename.txt` কে `main` branch থেকে টেনে এনে restore করবে।

---

# 🔹 Important Note

* Git 2.23 থেকে `git checkout` কে দুই ভাগে ভাগ করা হয়েছে, কারণ এটা অনেক কাজ একসাথে করত:

  * **`git switch`** → branch switch করার জন্য
  * **`git restore`** → file restore করার জন্য

👉 তবুও `git checkout` এখনও কাজ করে (backward compatibility)।

---

# ✅ Summary

* `git checkout branch` → branch change
* `git checkout -b branch` → নতুন branch তৈরি + switch
* `git checkout commit` → পুরনো commit দেখা
* `git checkout branch -- file` → নির্দিষ্ট file restore

---

👉 আপনি কি চান আমি একটা **visual diagram** বানাই যেখানে HEAD, branch pointer আর `git checkout` করলে কিভাবে নড়ে সেটা বোঝানো থাকবে?
