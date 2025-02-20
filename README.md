# githubCommand



01957@saddamnvn MINGW64 /h/githubCommand
$ <b> <p>git init</p></b>
<p>Initialized empty Git repository in H:/githubCommand/.git/</p>

01957@saddamnvn MINGW64 /h/githubCommand (master)
$<b><p>git remote add origin https://github.com/saddamsaddam/githubCommand.git</p></b>

01957@saddamnvn MINGW64 /h/githubCommand (master)
$<b> <p>git add .</p></b>

01957@saddamnvn MINGW64 /h/githubCommand (master)
$ <b><p>git commit -m "version 1.0.0"</p></b>
[master (root-commit) 5772790] version 1.0.0
 2 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 githubCommand.docx
 create mode 100644 ~$thubCommand.docx

01957@saddamnvn MINGW64 /h/githubCommand (master)
$<b><p> git push -u origin master</p></b>
Enumerating objects: 4, done.
Counting objects: 100% (4/4), done.
Delta compression using up to 8 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 9.69 KiB | 9.69 MiB/s, done.
Total 4 (delta 0), reused 0 (delta 0), pack-reused 0
To https://github.com/saddamsaddam/githubCommand.git
[new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.

You're encountering a **Permission denied (publickey)** error when trying to push to GitHub. This means GitHub is not recognizing your SSH key. Follow these steps to fix it:

### **1. Check if You Have an SSH Key**
Run the following command in PowerShell:
```powershell
ls ~/.ssh
```
If you see files like `id_rsa.pub` or `id_ed25519.pub`, you already have an SSH key.

### **2. Generate a New SSH Key (If Needed)**
If you don’t have an SSH key, generate one with:
```powershell
ssh-keygen -t ed25519 -C "your-email@example.com"
```
Replace `"your-email@example.com"` with your GitHub email. Press **Enter** through all prompts.

### **3. Add the SSH Key to GitHub**
Copy the key to the clipboard:
```powershell
Get-Content ~/.ssh/id_ed25519.pub | Set-Clipboard
```
(If you used RSA, replace `id_ed25519.pub` with `id_rsa.pub`.)

Then:
1. Go to **GitHub** → **Settings** → **SSH and GPG keys**.
2. Click **New SSH Key**.
3. Paste the key and save it.

### **4. Test the Connection**
Run:
```powershell
ssh -T git@github.com
```
If it says:
```
Hi saddamsaddam! You've successfully authenticated, but GitHub does not provide shell access.
```
Then your SSH key is working.

### **5. Retry Pushing to GitHub**
```powershell
git push -u origin master
```

This should work now! Let me know if you face any issues. 🚀




