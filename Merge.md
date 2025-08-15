give commit follow of main, sakib,rakib in merge


ঠিক আছে — এবার **merge** ব্যবহারের ক্ষেত্রে `main`, `sakib`, আর `rakib` ব্রাঞ্চের commit flow ধাপে ধাপে দেখাচ্ছি।

---

## 📜 Merge-based commit flow

### 1️⃣ শুরুতে অবস্থা

```
(main)  A---B
```

* `A` = প্রথম commit
* `B` = main এর সর্বশেষ commit

---

### 2️⃣ ব্রাঞ্চ তৈরি

```
(main)  A---B
          \     \
(sakib)    C     \
                 (rakib)    D
```

* Sakib এর নতুন commit = `C`
* Rakib এর নতুন commit = `D`

---

### 3️⃣ main-এ নতুন update (E)

```
(main)  A---B---E
          \     \
(sakib)    C     \
                 (rakib)    D
```

---

### 4️⃣ Merge sakib → main

`main` এবং `sakib` দুটোরই নতুন commit থাকায় Git **merge commit** তৈরি করবে:

```
(main)  A---B---E---M1
          \     /     
           C---/      
(rakib)           D
```

* `M1` = merge commit (Sakib এর পরিবর্তন `main`-এ আনলো)

---

### 5️⃣ Merge rakib → main

এবার `main`-এ আবার merge commit হবে:

```
(main)  A---B---E---M1---M2
          \     /     \   /
           C---/       D-/
```

* `M2` = merge commit (Rakib এর পরিবর্তন `main`-এ আনলো)

---

### 🔹 ফলাফল

* `main`-এর ইতিহাসে দুটি merge commit (`M1`, `M2`) আছে
* প্রতিটি ফিচার ব্রাঞ্চের আসল commit (`C`, `D`) তাদের আসল SHA-সহ main-এ এসেছে
* ইতিহাসে ব্রাঞ্চিং এবং মার্জিং এর রেখা দেখা যাবে (non-linear history)

---

💡 **পার্থক্য Rebase এর সাথে**:

* **Merge**: পুরনো SHA থাকে, merge commit যোগ হয়, ইতিহাস ব্রাঞ্চ আকারে থাকে
* **Rebase**: নতুন SHA হয়, merge commit লাগে না, ইতিহাস সোজা (linear) হয়

---







Alright — let’s walk through starting a **merge** again from your existing GitHub project.

Since you’re currently on `main` and up to date, you’ll first want a separate branch to merge.


https://www.youtube.com/watch?v=7B_km8LrkJw

<img width="852" height="427" alt="image" src="https://github.com/user-attachments/assets/19877518-9cd4-40c8-8a20-6949a97fa089" />

---

## 1️⃣ Create a feature branch and make a change

```bash
# Make sure you're on main and synced
git switch main
git pull origin main

# Create a feature branch
git switch -c feature/demo

# Make a change
echo "Hello from feature branch" > demo.txt
git add demo.txt
git commit -m "feat: add demo.txt file"
```

---

## 2️⃣ Push the branch to GitHub

```bash
git push -u origin feature/demo
```

You could open a PR on GitHub, **or** merge locally.

---

## 3️⃣ Merge into main locally

```bash
git switch main
git pull origin main          # make sure main is updated
git merge feature/demo        # merge commit will be created if needed
```

* If there’s no conflict, Git auto-merges.
* If there’s a conflict, Git will pause and ask you to resolve files, then:

```bash
git add <resolved-files>
git commit
```

---

## 4️⃣ Push the merged main branch Github

```bash
git push origin main
```

---

## 5️⃣ (Optional) Delete the feature branch after merge

```bash
git branch -d feature/demo            # delete local
git push origin --delete feature/demo # delete remote
```

---



merge er khetre ki  commits gulo main ses e jukto hobe, mane mone hobe lstes?


হ্যাঁ — **merge** করলে আপনার feature ব্রাঞ্চের commits গুলো `main` এর শেষে যুক্ত হবে, কিন্তু একটা ব্যাপার আছে:

---

## 1️⃣ Fast-forward merge হলে

যদি `main` এ আপনার feature ব্রাঞ্চ তৈরির পর থেকে **কোনও নতুন commit না আসে**, তাহলে merge করার সময় `main` সরাসরি feature এর শেষ commit এ চলে যাবে।

* এতে মনে হবে আপনার commits `main` এর latest হিসেবে যুক্ত হয়েছে।
* **কোনও extra merge commit তৈরি হবে না**।

**উদাহরণ:**

```
main:    A---B
feature: A---B---C---D

merge (fast-forward):
main:    A---B---C---D
```

---

## 2️⃣ 3-way merge (merge commit) হলে

যদি `main` এ feature branch তৈরির পর **নতুন commit এসে যায়**, তাহলে Git আপনার feature commits গুলো `main` এর সাথে merge করে একটি **merge commit** বানাবে।

**উদাহরণ:**

```
main:    A---B---E---F
feature: A---B---C---D

merge result:
main:    A---B---E---F---M
                   \     /
                    C---D
(M = merge commit)
```

* ইতিহাসে আপনার commits গুলো মূল ব্রাঞ্চের শেষে থাকে, কিন্তু merge commit এর পেছনে তারা দেখা যায়।
* Git log দেখতে গেলে বোঝা যাবে এগুলো কোথা থেকে এসেছে।

---

## 3️⃣ Rebase এর সাথে পার্থক্য

* **Merge:** commits গুলো তাদের আসল তারিখ ও SHA রেখেই যোগ হয়।
* **Rebase:** commits গুলোকে নতুন base এ বসিয়ে SHA পরিবর্তন করে, ফলে মনে হয় এগুলো latest এ লেখা হয়েছে।

---




