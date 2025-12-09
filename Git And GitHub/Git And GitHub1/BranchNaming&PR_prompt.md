# 📘 **Branch Naming Conventions Guide**

This document explains the standard rules for naming branches in our projects.
Following a consistent naming pattern keeps our workflow clean, readable, and easy to manage for everyone on the team.

---

## ## 🚀 **1. Branch Prefix Types**

Use one of the following prefixes depending on the type of work:

| Prefix                  | Purpose                                | Example                     |
| ----------------------- | -------------------------------------- | --------------------------- |
| **feat/**               | Adding a new feature                   | `feat/add-collections-ui`   |
| **fix/** or **bugfix/** | Fixing a bug                           | `fix/search-bar-delay`      |
| **ui/**                 | UI-related changes                     | `ui/update-collection-card` |
| **refactor/**           | Code cleanup without changing behavior | `refactor/pagination-logic` |
| **chore/**              | Maintenance tasks, config, or cleanup  | `chore/update-gitignore`    |
| **docs/**               | Documentation updates                  | `docs/update-readme`        |
| **test/**               | Test-related work                      | `test/add-api-tests`        |
| **hotfix/**             | Urgent production-level fix            | `hotfix/pagination-crash`   |

---

## ## ✏️ **2. Branch Naming Rules**

To maintain clarity and consistency:

### ✔ **Use lowercase letters only**

```
feat/add-search
```

### ✔ **Use hyphens (`-`) to separate words**

```
feat/create-collection-page
```

### ✔ **Start with the correct prefix**

```
feat/...
fix/...
ui/...
```

### ✔ **Keep names short but meaningful**

❌ `feat/working-on-many-changes`
✔️ `feat/add-search-filter`

### ✔ **Avoid personal names, spaces, or underscores**

❌ `feat/ram-update-ui`
✔️ `ui/update-home-layout`

### ✔ **Describe the task clearly**

Good:

```
feat/view-out-of-stock-products
```

Bad:

```
feat/work
```

---

## ## ⭐ **3. Good Branch Name Examples**

* `feat/view-out-of-stock-products` or `feat/view-oos-products`
* `feat/add-collection-search`
* `ui/update-setup-guide`
* `fix/pagination-not-working`
* `refactor/collection-fetch-logic`
* `chore/remove-unused-files`
* `docs/add-installation-instructions`

---

## ## 🔥 **4. Tips for Naming Better Branches**

* Think of the branch name as a *summary of your task*.
* Avoid long sentences—use 3–5 keywords max.
* Use abbreviations only when common (e.g., `oos` for *out of stock*).
* Be consistent—even small changes matter over time.

---

## ## 🎯 Final Recommendations

When creating a branch:

1. **Identify the work type** → choose the prefix
2. **Write a short but clear description**
3. **Use lowercase + hyphens**
4. **Double check readability before creating**

---

<br>

# 📄 **Standard PR Description Prompt **

Use this prompt when generating a PR description through ChatGPT:

```
Generate a clean and simple Pull Request description in Markdown using the following format:

## PR Description

### Summary
A short and clear explanation of what has been added or updated.

### What’s Done
A bullet-point list explaining the main features, changes, or improvements. 
Use simple English and keep it brief.

### Testing
Add points explaining what was tested and how the feature was verified.

---

The PR description should:
- Be easy to read
- Use Markdown headings and bullet points
- Avoid technical complexity unless necessary
- Follow the exact structure: Summary → What’s Done → Testing

Here is my code/task for reference:
[PASTE YOUR CODE OR EXPLAIN THE TASK HERE]
```

---