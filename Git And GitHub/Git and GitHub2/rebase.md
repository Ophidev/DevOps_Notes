
```markdown
# 🔄 Git Rebase — Complete Guide

Rebase is a powerful Git command that lets you **move commits from one branch on top of another branch**, creating a **linear, clean history**.  

This guide explains **what rebase is**, **how it works**, and **how it differs from merge** with diagrams and examples.

---

## 🧠 What is `git rebase`?

> `git rebase` = “move your commits on top of another branch”

- Takes commits from your current branch (e.g., `dev`)  
- Temporarily removes them  
- Applies commits from the target branch (e.g., `master`)  
- Reapplies your branch commits on top in sequence  

---

## 🎯 Example Scenario

Branches:

```

master: A --- B
dev:    A --- C --- D

````

- `master` has commit `B`  
- `dev` has commits `C` and `D`  

Run:

```bash
git checkout dev
git rebase master
````

---

### 🔹 What Happens

1. Git temporarily removes commits `C` and `D` from dev
2. Applies commits from master (`B`)
3. Reapplies `C` and `D` on top of `B`

Resulting history:

```
master: A --- B
dev:    A --- B --- C' --- D'
```

* Commits `C` and `D` get **new hashes** (`C'`, `D'`)
* History is now **linear**
* Master branch itself is **not changed**

---

## 🔹 Visual Mermaid Diagram

```mermaid
gitGraph
   commit id: "A" tag: "common ancestor"
   branch dev
   commit id: "C" tag: "dev commit 1"
   commit id: "D" tag: "dev commit 2"
   checkout master
   commit id: "B" tag: "master commit 1"
   checkout dev
   rebase master
```

After rebase:

```
master: A --- B
dev:    A --- B --- C' --- D'
```

---

## ⚙️ Rebase vs Merge — Simple Comparison

| Feature                     | Merge                       | Rebase                             |
| --------------------------- | --------------------------- | ---------------------------------- |
| Keeps both branch histories | ✅                           | ❌ (dev commits rewritten)          |
| Creates merge commit        | ✅                           | ❌ (history linear)                 |
| Master branch changes       | ✅ updated with merge commit | ❌ master stays unchanged           |
| Dev branch                  | Untouched                   | Commits rewritten on top of master |
| History style               | Branching preserved         | Linear, clean history              |

---

### 🔹 Think of it like this:

* **Merge:** Combines two lines of development → keeps history branched → may create a merge commit
* **Rebase:** Moves your branch commits on top of another branch → history looks like one straight line → no merge commit

---

### 🔹 Quick Visual

**Merge:**

```
master: A --- B -------- M
dev:        C --- D /
```

* M = merge commit

**Rebase:**

```
master: A --- B
dev:        C' --- D'
```

* Dev commits are rebased on top of master
* History is linear

---

## ⚠️ Handling Conflicts During Rebase

Conflicts can occur just like during merge:

```bash
git status          # Check conflicted files
nano file.txt       # Edit manually
git add file.txt    # Mark as resolved
git rebase --continue
```

* To cancel a rebase:

```bash
git rebase --abort
```

---

## 💡 Tips for Safe Rebase

* Rebase **rewrites commit history**, so **avoid rebasing shared branches**
* After rebasing a branch that’s already shared, you may need to **force push** (`git push -f`)
* Use `git log --oneline --graph` to visualize linear history
* Rebase before merging to keep your project history **clean and readable**

---

## 🌈 Summary

* `git rebase` = replay your commits on top of another branch
* Creates a **linear history** without merge commits
* Dev branch is rewritten (new commit hashes)
* Master remains unchanged during rebase
* Conflicts are resolved manually just like merge

> 🎯 **Tip:** Use rebase for a clean project history, use merge when you want to preserve branch structure. 🚀

```

---
                        