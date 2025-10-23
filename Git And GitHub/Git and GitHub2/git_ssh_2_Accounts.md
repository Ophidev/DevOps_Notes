---

# 🐙 GitHub Multi-Account Setup on Windows

A complete guide to using **two GitHub accounts** on the same PC using **HTTPS for default account** and **SSH for a second account**.

---

## 🎯 Goal

* Use **Account A** (default/global) with HTTPS
* Use **Account B** (secondary) with SSH
* Push and pull without conflicts or changing global config

---

## 📂 Folder Structure

```text
C:\Users\bhatt\.ssh\
├─ config             # SSH config for secondary account
├─ id_ed25519_second  # Private key for second account
├─ id_ed25519_second.pub  # Public key for second account
├─ known_hosts
```

---

## 🔑 Step 1: Generate SSH Key for Second Account

```powershell
ssh-keygen -t ed25519 -C "bhattadi60@gmail.com" -f H:\.ssh\id_ed25519_second
```

* `-t ed25519` → Key type (modern & secure)
* `-C` → Comment (email to identify key)
* `-f` → Path/filename for the key (H: drive here)
* Press Enter twice if no passphrase is needed

**Check keys:**

```powershell
ls H:\.ssh
```

---

## 📋 Step 2: Add Public Key to GitHub (Account B)

```powershell
type H:\.ssh\id_ed25519_second.pub
```

* Copy output
* GitHub → Settings → SSH and GPG Keys → New SSH Key → Paste

---

## 📝 Step 3: SSH Config File

File location: `C:\Users\bhatt\.ssh\config`

```text
# Second GitHub account (Account B)
Host github-second
    HostName github.com
    User git
    IdentityFile H:\.ssh\id_ed25519_second
    IdentitiesOnly yes
```

> Note: Account A uses HTTPS, no SSH needed.

**Rename file correctly** if using Notepad (`config.txt` → `config`).

---

## 🔧 Step 4: Test SSH Connection

```powershell
ssh -T git@github-second
```

Expected output:

```
Hi AdityaBhatt37! You've successfully authenticated, but GitHub does not provide shell access.
```

> SSH test for Account A will fail (Permission denied) because it uses HTTPS.

---

## 📦 Step 5: Cloning Repos

### ✅ Default Account (Account A) → HTTPS

```powershell
git clone https://github.com/usernameA/repo.git
```

* Uses global Git config (`git config --global user.name/email`)
* Authenticate via username + Personal Access Token (PAT)

### ✅ Second Account (Account B) → SSH

```powershell
git clone git@github-second:usernameB/repo.git
```

* Uses SSH key specified in `config`
* Optional: set **local Git config** for this repo:

```powershell
cd repo-for-accountB
git config user.name "Aditya Bhatt"
git config user.email "bhattadi60@gmail.com"
```

---

## 🌀 Workflow Diagram

```mermaid
flowchart LR
    A[Default Account (HTTPS)] -->|Clone/Pull/Push| RepoA[Repo A]
    B[Second Account (SSH)] -->|Clone/Pull/Push| RepoB[Repo B]
    RepoA -->|Global Git Config| Git[Git]
    RepoB -->|Local Git Config + SSH Key| Git
```

---

## 💡 Notes & Tips

* Account A continues using **HTTPS**, no SSH needed.
* Account B uses **SSH with alias** in `config`.
* Use **local Git config** for Account B repos to override global settings.
* You can store SSH keys on any drive (`H:` in this example).
* Always keep private keys safe!

---

## 📌 Command Summary

| Command                                      | Purpose                    | Notes                                       |
| -------------------------------------------- | -------------------------- | ------------------------------------------- |
| `ssh-keygen -t ed25519 -C "email" -f <path>` | Generate SSH key           | `-t` type, `-C` comment, `-f` path+filename |
| `type <key.pub>`                             | Show public key            | Copy to GitHub                              |
| `ssh-add <private_key>`                      | Add key to SSH agent       | Optional, auto-used if in config            |
| `ssh -T git@github-second`                   | Test SSH connection        | Should authenticate Account B               |
| `git clone https://github.com/...`           | Clone default account repo | Uses HTTPS                                  |
| `git clone git@github-second:...`            | Clone second account repo  | Uses SSH + config alias                     |
| `git config user.name/email`                 | Set local Git user         | Overrides global config per repo            |

---

## 🎉 Result

* **Account A** → HTTPS, global config
* **Account B** → SSH, alias `github-second`, local config per repo
* Both coexist seamlessly on the same PC!


