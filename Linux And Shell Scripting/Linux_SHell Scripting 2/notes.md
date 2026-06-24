
# 🌟 DEVOPS 3 – Linux & Shell Scripting

In this lecture, we are going to learn about the following topics:

1. User Management 👤
2. User Groups 👥
3. Sudo 🛡️
4. grep 🔍
5. awk 📄
6. ACL (Access Control List) 🔑
7. SSH (Secure Shell) & SCP (Server Copy) 🖥️
8. System CTC ⚙️

---

## 📝 1️⃣ User Management

### Creating a New User

```bash
ophid@MORK:/mnt/h/MORK/ophidubantu$ whoami
ophid

ophid@MORK:/mnt/h/MORK/ophidubantu$ useradd ayush-dev -m
useradd: Permission denied.
useradd: cannot lock /etc/passwd; try again later.
````

* `-m` → Creates `/home/username` directory for the new user.
* Normal users **cannot** create users. You must be a **superuser** (root).
* `/etc/passwd` → Contains all user information.

✅ **Correct way using sudo:**

```bash
sudo useradd ayush-dev -m
sudo cat /etc/passwd
```

* Example `/etc/passwd` output shows all users on the machine.

### Setting Password for User

```bash
sudo passwd ayush-dev
```

* Now user `ayush-dev` has a password set.

### Switching Users

```bash
su ayush-dev
whoami
cd /home/ayush-dev
mkdir dev_files
cd dev_files
touch dev_file.txt
ls
exit
```

* `su` → Switch to another user.
* `exit` → Returns to original user.
* **Linux security:** Users cannot access other users’ home directories by default.

---

### Creating Multiple Users

```bash
sudo useradd ophid-dev
sudo passwd ophid-dev
sudo useradd ophid-tester
sudo passwd ophid-tester
sudo useradd ophid-devops
sudo passwd ophid-devops
```

* Use `sudo cat /etc/passwd` to see all users.

---

## 📝 2️⃣ User Groups

### Creating a Group

```bash
sudo groupadd devops
sudo cat /etc/group
```

* Linux treats each user as a group by default.
* Groups are used to **share resources** among users.

### Adding Users to Groups

```bash
# Add a single user
sudo gpasswd -a ophid-dev devops

# Add multiple users (overwrites group members)
sudo gpasswd -M ophid-devops,ayush-dev devops

# Append users without overwriting
sudo gpasswd -a ophid devops
```

**Tip:** Use `-a` to append users. Use `-M` carefully — it overwrites existing members.

**Current devops group:**

```
devops:x:1005:ophid-dev,ayush-dev,ophid-devops,ophid
```

---

## 📝 3️⃣ Sudo

* `/etc/sudoers` → Configuration file for system permissions.
* `%sudo ALL=(ALL:ALL) ALL` → Members of sudo group can execute any command.
* Adding our devops group:

```text
%devops ALL=(ALL) ALL
```

* `%` → Indicates a **group**.
* All members of `devops` now have root privileges.

✨ **Tip:** After editing `/etc/sudoers`, reboot with:

```bash
sudo reboot
```

---

# 🔐 Linux File Permissions, chmod & chown Notes

---

# 📌 Why File Permissions Matter

Linux is a multi-user operating system.

Permissions control:

* Who can read files
* Who can edit files
* Who can execute programs
* Security between users/services
* Team/project access

Very important in:

* DevOps
* Docker
* Linux Administration
* CI/CD
* Production servers
* Nginx/Apache
* Kubernetes

---

# 📁 Linux Permission Model

Every file/folder has:

```text
1. Owner User
2. Owner Group
3. Others
```

Example:

```bash
ls -la
```

Output:

```bash
-rw-rw-r-- 1 ophid-dev developers 0 May 14 dev_file.txt
```

---

# 🔍 Breakdown of Output

```text
-rw-rw-r-- 1 ophid-dev developers 0 May 14 dev_file.txt
```

| Part           | Meaning            |
| -------------- | ------------------ |
| `-`            | File type          |
| `rw-`          | Owner permissions  |
| `rw-`          | Group permissions  |
| `r--`          | Others permissions |
| `1`            | Hard links         |
| `ophid-dev`   | Owner user         |
| `developers`   | Owner group        |
| `0`            | File size          |
| `May 14`       | Last modified date |
| `dev_file.txt` | File name          |

---

# 📂 File Types

| Symbol | Meaning          |
| ------ | ---------------- |
| `-`    | Regular file     |
| `d`    | Directory        |
| `l`    | Symbolic link    |
| `c`    | Character device |
| `b`    | Block device     |

Example:

```bash
drwxr-xr-x
```

`d` means directory.

---

# 🔑 Permission Meaning

| Symbol | Meaning       |
| ------ | ------------- |
| `r`    | Read          |
| `w`    | Write         |
| `x`    | Execute       |
| `-`    | No permission |

---

# 👤 Permission Sections

Example:

```bash
-rwxr-x---
```

Breakdown:

```text
Owner  → rwx
Group  → r-x
Others → ---
```

---

# 🔢 Numeric Permission System

Linux converts permissions into numbers.

| Permission | Value |
| ---------- | ----- |
| `r`        | 4     |
| `w`        | 2     |
| `x`        | 1     |

Add values together.

---

# 📌 Common Permission Numbers

| Number | Meaning |
| ------ | ------- |
| `7`    | rwx     |
| `6`    | rw-     |
| `5`    | r-x     |
| `4`    | r--     |
| `0`    | ---     |

---

# 🧠 Easy Permission Calculation

## Example: `750`

```text
7 = 4+2+1 = rwx
5 = 4+1   = r-x
0 = ---
```

Final:

```text
Owner  → rwx
Group  → r-x
Others → ---
```

---

# 🔥 chmod Command

`chmod` means:

```text
change mode (permissions)
```

Syntax:

```bash
chmod [permissions] filename
```

---

# 📌 chmod Examples

## 700

```bash
chmod 700 dev_file.txt
```

Meaning:

| Section | Permission |
| ------- | ---------- |
| Owner   | rwx        |
| Group   | ---        |
| Others  | ---        |

Only owner has full access.

---

## 750

```bash
chmod 750 dev_file.txt
```

Meaning:

| Section | Permission |
| ------- | ---------- |
| Owner   | rwx        |
| Group   | r-x        |
| Others  | ---        |

---

## 755 (VERY COMMON)

```bash
chmod 755 script.sh
```

Meaning:

| Section | Permission |
| ------- | ---------- |
| Owner   | rwx        |
| Group   | r-x        |
| Others  | r-x        |

Very common for:

* scripts
* websites
* executable files

---

## 644 (VERY COMMON)

```bash
chmod 644 file.txt
```

Meaning:

| Section | Permission |
| ------- | ---------- |
| Owner   | rw-        |
| Group   | r--        |
| Others  | r--        |

Very common for:

* config files
* source code
* text files

---

# 📂 chmod on Directories

Directories behave differently.

| Permission | Meaning                |
| ---------- | ---------------------- |
| `r`        | View files inside      |
| `w`        | Create/delete files    |
| `x`        | Enter directory (`cd`) |

---

# 📌 Directory Example

```bash
chmod 755 myfolder
```

Allows:

* everyone can enter folder
* everyone can view files
* only owner can modify

---

# 🔁 Recursive chmod

Use `-R` for recursive.

```bash
chmod -R 755 project/
```

Applies permissions to:

* all files
* subfolders
* nested content

---

# 👑 chown Command

`chown` means:

```text
change ownership
```

Used to change:

* owner user
* owner group

---

# 📌 chown Syntax

```bash
chown user file
```

Example:

```bash
sudo chown ophid-dev dev_file.txt
```

Changes file owner.

---

# 📌 Change Owner + Group

Syntax:

```bash
chown user:group file
```

Example:

```bash
sudo chown ophid-dev:developers dev_file.txt
```

Meaning:

* owner user = ophid-dev
* owner group = developers

---

# 📌 Change Only Group

```bash
sudo chown :developers dev_file.txt
```

Changes only group.

---

# 📌 Alternative Group Command

```bash
chgrp developers dev_file.txt
```

`chgrp` means:

```text
change group
```

---

# 🔁 Recursive chown

```bash
sudo chown -R ophid-dev:developers project/
```

Recursively changes:

* all files
* all folders

Very common in:

* web servers
* Docker volumes
* DevOps deployments

---

# 👥 Linux Groups Practical Use

Groups are permission teams.

Example:

```text
developers
sudo
docker
www-data
```

Instead of giving permissions user-by-user,
Linux uses groups.

---

# 📌 Docker Group Example (VERY IMPORTANT)

Normally:

```bash
sudo docker ps
```

After adding user to docker group:

```bash
sudo usermod -aG docker username
```

Now:

```bash
docker ps
```

works WITHOUT sudo.

Very common DevOps interview topic.

---

# 👥 usermod Breakdown

Example:

```bash
sudo usermod -aG docker ophid-dev
```

| Part         | Meaning              |
| ------------ | -------------------- |
| `usermod`    | modify user          |
| `-a`         | append               |
| `-G`         | supplementary groups |
| `docker`     | group name           |
| `ophid-dev` | username             |

Meaning:

```text
Add user to docker group without removing existing groups.
```

---

# ⚠️ VERY IMPORTANT

## WRONG:

```bash
sudo usermod -G docker username
```

This REPLACES all supplementary groups.

---

## CORRECT:

```bash
sudo usermod -aG docker username
```

Always use:

```text
-aG
- G stands for supplementary groups which means secondary groups, means add user/ modify user and add in extra group and don't touch the primary group.
```

---

# 🧠 Primary vs Supplementary Groups

Every user has:

| Type                 | Meaning                 |
| -------------------- | ----------------------- |
| Primary Group        | Main/default group      |
| Supplementary Groups | Extra permission groups |

---

# 📌 Check User Groups

```bash
id username
```

Example:

```bash
id ophid-dev
```

Output:

```bash
uid=1000(ophid-dev)
gid=1000(ophid-dev)
groups=1000(ophid-dev),27(sudo),999(docker)
```

---

# 🔐 Important DevOps Permissions

| Permission | Usage                   |
| ---------- | ----------------------- |
| `755`      | scripts/web folders     |
| `644`      | config/source files     |
| `600`      | secret/private files    |
| `700`      | private folders/scripts |

---

# ⚠️ Security Best Practices (IMPORTANT)

## NEVER Use:

```bash
chmod 777
```

unless absolutely necessary.

Why?

```text
Everyone gets full permissions.
```

Very insecure.

---

# 🚨 DevOps Interview Important Questions

## Q1: Difference between chmod and chown?

| Command | Purpose            |
| ------- | ------------------ |
| `chmod` | change permissions |
| `chown` | change ownership   |

---

## Q2: Difference between primary and supplementary groups?

| Type          | Meaning                 |
| ------------- | ----------------------- |
| Primary       | default/main group      |
| Supplementary | extra permission groups |

---

## Q3: Why use groups?

Groups allow:

* team-based permissions
* easier access management
* secure shared folders
* scalable administration

---

## Q4: Why add user to docker group?

To run Docker commands without sudo.

---

## Q5: What does chmod 755 mean?

```text
Owner  → rwx
Group  → r-x
Others → r-x
```

---

# 📌 Useful Commands Summary

## View Permissions

```bash
ls -l
ls -la
```

---

## Change Permissions

```bash
chmod 755 file
chmod -R 755 folder
```

---

## Change Ownership

```bash
chown user file
chown user:group file
```

---

## Change Group

```bash
chgrp group file
```

---

## Add User to Group

```bash
sudo usermod -aG docker username
```

---

## Check User Groups

```bash
groups username
id username
```

---

# 🧠 Easy Memory Tricks

## chmod

```text
change mode (permissions)
```

---

## chown

```text
change ownership
```

---

## chgrp

```text
change group
```

---

## usermod -aG

```text
Append user to supplementary Groups
```

---

# ✅ Final Core Understanding

```text
chmod  → controls permissions
chown  → controls ownership
groups → manage team access
```

Linux security is mainly built around:

* users
* groups
* permissions
* ownership


---

## 📝 5️⃣ ACL (Access Control List)

* ACL (Access Control List) is an advanced permission system in Linux used to give specific permissions to specific users or groups on files/directories without changing ownership or traditional chmod permissions.

### Installing ACL

```bash
sudo apt-get install acl
```

* ACL allows **specific permissions** for specific users without changing ownership.

### Commands

```bash
# Get ACL of a file
getfacl dev_file.txt

# Set ACL for user
sudo setfacl -m u:ophid:rwx dev_file.txt
```

* `getfacl` → Get current permissions.
* `setfacl` → Set permissions for specific users.

```bash
whoami
echo "user ophid is writing in dev_file.txt" > dev_file.txt
cat dev_file.txt
```

* ACL allows `ophid` to read/write/execute without changing owner.

---


# 📝 6️⃣ grep (Global Regular Expression Print)

## 📌 Definition

`grep` is a Linux command used to search specific text, patterns, or strings inside files and directories.

Very important in:

* DevOps
* Log analysis
* Monitoring
* CI/CD
* Debugging
* Linux administration

---

# 🧠 Easy Understanding

```text
grep = search engine for text inside Linux
```

---

# 📌 Basic Syntax

```bash
grep "pattern" file
```

---

# 📌 Search in Specific File

```bash
grep "devops" /home/ophid-dev/dev_files/dev_file.txt
```

Searches:

* word `devops`
* inside specific file

---

# 📌 Recursive Search

```bash
grep -r "devops" /home
```

## Breakdown

| Option | Meaning          |
| ------ | ---------------- |
| `-r`   | recursive search |

Searches:

* all folders
* subfolders
* files recursively

---

# 📌 Case Insensitive Search

```bash
grep -ri "devops" /home/ophid-dev/dev_files
```

## Breakdown

| Option | Meaning          |
| ------ | ---------------- |
| `-r`   | recursive        |
| `-i`   | case insensitive |

Matches:

* DevOps
* DEVOPS
* devops

---

# 📌 Show Line Numbers

```bash
grep -n "ERROR" logs.txt
```

Example output:

```text
2:ERROR DB Failed
5:ERROR Login Failed
```

`-n` → show line numbers.

---

# 📌 Invert Match

```bash
grep -v "INFO" logs.txt
```

Shows lines NOT containing INFO.

---

# 📌 Count Matching Lines

```bash
grep -c "ERROR" logs.txt
```

Counts total matching lines.

---

# 📌 Match Exact Word

```bash
grep -w "devops" file.txt
```

Avoids partial matches.

Example:

* matches `devops`
* not `devops123`

---

# 📌 Show Only Matching Filenames

```bash
grep -l "ERROR" *.log
```

Shows filenames containing ERROR.

---

# 📌 Using grep with Pipe `|`

```bash
ps aux | grep nginx
```

Search running nginx processes.

VERY common DevOps command.

---

# 📌 Check User Exists

```bash
sudo grep ophid-dev /etc/passwd
```

Search user entry inside passwd file.

---

# 📌 Real DevOps Examples

## Search Errors

```bash
grep "ERROR" app.log
```

---

## Search Docker Containers

```bash
docker ps | grep nginx
```

---

## Search Environment Variables

```bash
env | grep PATH
```

---

# 🚨 grep Interview Questions

## Q1: Difference between grep and find?

| Command | Purpose                  |
| ------- | ------------------------ |
| `grep`  | search text inside files |
| `find`  | search files/directories |

---

## Q2: What does `-r` mean?

Recursive search.

---

## Q3: What does `-i` mean?

Case-insensitive search.

---

# 🧠 Easy Memory

```text
grep = search text/pattern
```

---

# 📝 7️⃣ find Command

# 📌 Definition

`find` is a Linux command used to search files and directories based on conditions like:

* name
* size
* permissions
* owner
* modification time

Very important in:

* DevOps
* log cleanup
* security auditing
* file management
* automation

---

# 🧠 Easy Understanding

```text
find = locate files/folders
```

---

# 📌 Basic Syntax

```bash
find [path] [condition]
```

---

# 📌 Find Files with 777 Permissions

```bash
find /home -type f -perm 777
```

## Breakdown

| Option      | Meaning           |
| ----------- | ----------------- |
| `-type f`   | only files        |
| `-perm 777` | permission filter |

Very useful for:

* security audits
* insecure file detection

---

# 📌 Find `.log` Files

```bash
find /home -type f -name "*.log"
```

Searches all `.log` files.

---

# 📌 File Types

| Option    | Meaning   |
| --------- | --------- |
| `-type f` | file      |
| `-type d` | directory |

---

# 📌 Find Directories

```bash
find /home -type d -name "project"
```

---

# 📌 Find Large Files

```bash
find /var/log -size +100M
```

Find files larger than 100MB.

---

# 📌 Find Small Files

```bash
find /tmp -size -1M
```

Find files smaller than 1MB.

---

# 📌 Find by User

```bash
find /home -user ophid
```

Search files owned by user.

---

# 📌 Find by Group

```bash
find /home -group devops
```

---

# 📌 Find Recently Modified Files

```bash
find /logs -mtime -7
```

Files modified within last 7 days.

---

# 📌 Find Old Files

```bash
find /logs -mtime +30
```

Files older than 30 days.

---

# 📌 Find Empty Files

```bash
find /tmp -empty
```

---

# 📌 Execute Command on Found Files

```bash
find /home -name "*.log" -exec rm {} \\;
```

## Breakdown

| Part    | Meaning            |
| ------- | ------------------ |
| `-exec` | execute command    |
| `{}`    | current file       |
| `\\;`   | command terminator |

VERY powerful and dangerous.

---

# 📌 Delete Found Files

```bash
find /tmp -name "*.tmp" -delete
```

---

# 📌 Real DevOps Examples

## Find Large Logs

```bash
find /var/log -size +1G
```

---

## Find Permission Issues

```bash
find / -perm 777
```

---

## Cleanup Old Logs

```bash
find /logs -mtime +30 -delete
```

---

# 🚨 find Interview Questions

## Q1: Difference between grep and find?

| Command | Purpose      |
| ------- | ------------ |
| `grep`  | search text  |
| `find`  | search files |

---

## Q2: What does `-exec` do?

Executes command on matched files.

---

## Q3: What does `-mtime` mean?

Modification time filter.

---

# 🧠 Easy Memory

```text
find = locate/search files
```

---

# 📝 8️⃣ awk Command

# 📌 Definition

`awk` is a powerful Linux text-processing tool used to:

* filter
* format
* extract
* analyze structured text data

Very important for:

* logs
* CSV files
* monitoring
* DevOps automation

---

# 🧠 Easy Understanding

```text
awk = mini programming language for text
```

---

# 📌 awk Works Column-Wise

Example file:

```text
ophid DevOps 50000
Ayush Backend 60000
Rohit Frontend 45000
```

| Column | Meaning       |
| ------ | ------------- |
| `$1`   | first column  |
| `$2`   | second column |
| `$3`   | third column  |

---

# 📌 Print Specific Columns

```bash
awk '{print $1,$3}' employee.txt
```

Output:

```text
ophid 50000
Ayush 60000
Rohit 45000
```

---

# 📌 Print Full Line

```bash
awk '{print $0}' file.txt
```

`$0` means entire row.

---

# 📌 NR (Row Number)

```bash
awk '{print NR,$1}' file.txt
```

Example:

```text
1 ophid
2 Ayush
3 Rohit
```

---

# 📌 NF (Number of Fields)

```bash
awk '{print NF}' file.txt
```

Prints number of columns.

---

# 📌 Search ERROR Logs

```bash
awk '/ERROR/ {print NR,$1,$2,$4}' log_file.txt
```

## Breakdown

| Part       | Meaning            |
| ---------- | ------------------ |
| `/ERROR/`  | filter ERROR lines |
| `NR`       | row number         |
| `$1,$2,$4` | selected columns   |

---

# 📌 Filter Rows by Condition

```bash
awk 'NR>1 && NR<10 && /ERROR/ {print NR}' log_file.txt
```

Meaning:

* rows between 1 and 10
* containing ERROR

---

# 📌 Save Filtered Output

```bash
touch Error_upto_50.txt

awk 'NR>0 && NR<51 && /ERROR/ {print NR,$1,$2,$4,$5,$6}' log_file.txt > Error_upto_50.txt
```

---

# 📌 BEGIN Block

```bash
awk 'BEGIN {print "Start"} {print $1}' file.txt
```

Runs before processing.

---

# 📌 END Block

```bash
awk 'END {print NR}' file.txt
```

Print total rows after processing.

---

# 📌 Count Total Lines

```bash
awk 'END {print NR}' file.txt
```

---

# 📌 Real DevOps Examples

## Extract IP Addresses

```bash
awk '{print $1}' access.log
```

---

## Extract CPU Usage

```bash
top | awk '{print $1,$9}'
```

---

## Analyze Error Logs

```bash
awk '/ERROR/' app.log
```

---

# 🚨 awk Interview Questions

## Q1: Difference between grep and awk?

| Command | Purpose              |
| ------- | -------------------- |
| `grep`  | search text          |
| `awk`   | process/extract text |

---

## Q2: What is `$1` in awk?

First column.

---

## Q3: What is `NR`?

Current row number.

---

## Q4: What is `$0`?

Entire row/line.

---

# 🧠 Easy Memory

```text
grep → searching
find → locating
awk → analyzing text
```

---

# ⭐ MOST IMPORTANT FINAL UNDERSTANDING

| Command | Main Job                 |
| ------- | ------------------------ |
| `grep`  | search text/pattern      |
| `find`  | search files/directories |
| `awk`   | process structured text  |

