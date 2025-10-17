# 🧠 DevOps Practice 50 – Linux & Shell Scripting Mastery

A complete set of **50 practical Linux + Shell Scripting questions** designed to help you remember and use every major command from DevOps Notes (Part 2, 3 & 4). Each question reinforces a real-world DevOps concept.

---

## 🧩 Section 1: Linux Basics (Commands & Navigation)

1. Which command shows the **current working directory**?
2. How can you **list all files (including hidden ones)** in long format?
3. What command is used to **create a new directory** named `test_dir`?
4. How do you **remove** a directory named `logs` **with all its contents**?
5. How can you **copy** a file `app.conf` to `/etc/backup`?
6. How do you **move** `file1.txt` from `/tmp` to `/home/dev/`?
7. What command will show the **first 10 lines** of a file named `system.log`?
8. Which command helps you view large files **one page at a time**?
9. How do you **print the last 15 lines** of a log file?
10. How do you **view contents** of `/etc/passwd` file quickly?

---

## 🔐 Section 2: Permissions & Ownership

11. What is the **numerical permission** for `rwxr-xr-x`?
12. Which command gives **execute permission** to the owner of `script.sh`?
13. How do you **change ownership** of `devops.txt` to user `aditya` and group `devops`?
14. What is the **symbolic meaning** of permission `644`?
15. How can you **grant read, write, and execute** permission to user `ayush` on file `dev_file.txt` using ACL?

---

## 👤 Section 3: User Management

16. What command creates a user `ayush-dev` with a **home directory**?
17. How do you **set a password** for user `ayush-dev`?
18. Which command lets you **switch** to another user `ayush-dev`?
19. How do you **check your current username** in the terminal?
20. Where are **user account details** stored in Linux?
21. How do you **add multiple users** named `aditya-dev` and `aditya-tester`?
22. Which command allows you to **exit** from a switched user session?

---

## 👥 Section 4: Groups & Sudo

23. How do you **create a group** named `devops`?
24. How do you **add a user** `aditya-dev` to `devops` group?
25. How can you **add multiple users** `aditya-devops` and `ayush-dev` to the `devops` group at once?
26. Where can you **view all existing groups** in the system?
27. How do you open the **sudoers file** safely for editing?
28. Which line should you add to **grant sudo access** to the `devops` group?
29. Which command **restarts the system** after changes in `sudoers`?

---

## 🔑 Section 5: ACL – Access Control List

30. What command installs **ACL package** on Ubuntu?
31. How can you **grant user `aditya` rwx access** to `dev_file.txt`?
32. How do you **check ACL permissions** for a file?
33. Why is ACL useful compared to normal permissions?

---

## 🔍 Section 6: Searching Commands

34. Write a command to **find the word "devops"** inside `team.txt`.
35. How can you **recursively search** for `"error"` inside `/var/log/`?
36. How can you **ignore case sensitivity** while searching `"ssh"` in `/etc/`?
37. How do you **search for files** ending with `.log` inside `/home`?
38. Write a command to **find all files with 777 permissions** in the root directory.
39. How do you **find all `.log` files modified in the last 24 hours** inside `/var/log`?

---

## 📄 Section 7: awk Command

40. Write an `awk` command to **print line number, first, second, and fourth column** for lines containing `"ERROR"` in `log.txt`.
41. How can you **print lines between 2 and 9 containing “WARN”** from `syslog`?
42. How can you **save the first 50 lines containing “ERROR”** into a new file called `Error_upto_50.txt`?

---

## ⚙️ Section 8: systemctl, systemd & Daemons

43. What is the command to **start**, **stop**, and **restart** the Docker service?
44. How do you **enable Docker service** to start automatically on boot?
45. Which command shows the **status** of a running service like Docker?
46. How can you **list all active services** in your system?
47. Where are most `.service` files stored in Linux?
48. Write the name of the **daemon** responsible for task scheduling.
49. What is the command to **view CPU usage live** in Linux?
50. Which command helps you **list currently logged-in users with headers**?

---

## ✅ Bonus Challenge

Create a shell script named `devops_practice.sh` that:

* Creates a folder `practice_dir`
* Inside it, creates 3 files (`a.txt`, `b.txt`, `c.txt`)
* Sets ACL for a user `testuser` to have rwx access on all
* Lists disk usage and memory usage in one line
* Searches all `.sh` files in `/home` modified today

---

### ✍️ Author

**Ophid**
*DevOps & Backend Engineer – Linux | Cloud | Automation*
