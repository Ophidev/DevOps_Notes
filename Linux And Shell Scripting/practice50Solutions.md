# 🧠 DevOps Practice 50 Answers – Linux & Shell Scripting Mastery

This file contains **detailed answers and explanations** for all 50 DevOps practice questions from `practice50.md`.

---

## 🧩 Section 1: Linux Basics (Commands & Navigation)

1. **Current working directory:**

   ```bash
   pwd
   ```

2. **List all files (including hidden) in long format:**

   ```bash
   ls -la
   ```

3. **Create a new directory:**

   ```bash
   mkdir test_dir
   ```

4. **Remove a directory with all contents:**

   ```bash
   rm -rf logs
   ```

5. **Copy file to directory:**

   ```bash
   cp app.conf /etc/backup/
   ```

6. **Move a file:**

   ```bash
   mv /tmp/file1.txt /home/dev/
   ```

7. **First 10 lines of a file:**

   ```bash
   head system.log
   ```

8. **View large file page by page:**

   ```bash
   less bigfile.log
   ```

9. **Last 15 lines of a file:**

   ```bash
   tail -n 15 logfile.log
   ```

10. **Quickly view contents of a file:**

    ```bash
    cat /etc/passwd
    ```

---

## 🔐 Section 2: Permissions & Ownership

11. **rwxr-xr-x numeric value:** `755`

12. **Give execute permission to owner:**

    ```bash
    chmod u+x script.sh
    ```

13. **Change ownership:**

    ```bash
    chown aditya:devops devops.txt
    ```

14. **Permission 644 meaning:**

    * Owner: read + write
    * Group: read
    * Others: read

15. **Grant rwx using ACL:**

    ```bash
    setfacl -m u:ayush:rwx dev_file.txt
    ```

---

## 👤 Section 3: User Management

16. **Create user with home directory:**

    ```bash
    useradd -m ayush-dev
    ```

17. **Set password for user:**

    ```bash
    passwd ayush-dev
    ```

18. **Switch to another user:**

    ```bash
    su - ayush-dev
    ```

19. **Check current username:**

    ```bash
    whoami
    ```

20. **User account details file:** `/etc/passwd`

21. **Add multiple users:**

    ```bash
    useradd aditya-dev
    useradd aditya-tester
    ```

22. **Exit from switched user:**

    ```bash
    exit
    ```

---

## 👥 Section 4: Groups & Sudo

23. **Create a group:**

    ```bash
    groupadd devops
    ```

24. **Add user to group:**

    ```bash
    usermod -aG devops aditya-dev
    ```

25. **Add multiple users to group:**

    ```bash
    usermod -aG devops aditya-devops
    usermod -aG devops ayush-dev
    ```

26. **View all existing groups:**

    ```bash
    cat /etc/group
    ```

27. **Open sudoers file safely:**

    ```bash
    visudo
    ```

28. **Grant sudo access to devops group:**

    ```
    %devops ALL=(ALL:ALL) ALL
    ```

29. **Restart system after sudoers change:**

    ```bash
    reboot
    ```

---

## 🔑 Section 5: ACL – Access Control List

30. **Install ACL package (Ubuntu):**

    ```bash
    sudo apt install acl -y
    ```

31. **Grant user rwx access:**

    ```bash
    setfacl -m u:aditya:rwx dev_file.txt
    ```

32. **Check ACL permissions:**

    ```bash
    getfacl dev_file.txt
    ```

33. **Why ACL is useful:**

    * It allows setting **fine-grained permissions** for multiple users without changing ownership or main permission bits.

---

## 🔍 Section 6: Searching Commands

34. **Find word in a file:**

    ```bash
    grep "devops" team.txt
    ```

35. **Recursively search in a directory:**

    ```bash
    grep -r "error" /var/log/
    ```

36. **Ignore case while searching:**

    ```bash
    grep -ri "ssh" /etc/
    ```

37. **Find files ending with .log:**

    ```bash
    find /home -type f -name "*.log"
    ```

38. **Find all files with 777 permission:**

    ```bash
    find / -type f -perm 777
    ```

39. **Find .log files modified in last 24 hours:**

    ```bash
    find /var/log -type f -name "*.log" -mtime -1
    ```

---

## 📄 Section 7: awk Command

40. **Print line number, 1st, 2nd, 4th column with 'ERROR':**

    ```bash
    awk '/ERROR/ {print NR, $1, $2, $4}' log.txt
    ```

41. **Print lines between 2 and 9 containing 'WARN':**

    ```bash
    awk 'NR>=2 && NR<=9 && /WARN/' syslog
    ```

42. **Save first 50 ERROR lines to file:**

    ```bash
    awk '/ERROR/ && NR<=50' log.txt > Error_upto_50.txt
    ```

---

## ⚙️ Section 8: systemctl, systemd & Daemons

43. **Start / Stop / Restart Docker:**

    ```bash
    sudo systemctl start docker
    sudo systemctl stop docker
    sudo systemctl restart docker
    ```

44. **Enable Docker to start on boot:**

    ```bash
    sudo systemctl enable docker
    ```

45. **Show status of a service:**

    ```bash
    sudo systemctl status docker
    ```

46. **List all active services:**

    ```bash
    systemctl list-units --type=service --state=active
    ```

47. **Location of service files:** `/etc/systemd/system/` and `/usr/lib/systemd/system/`

48. **Daemon for scheduling tasks:** `cron`

49. **View live CPU usage:**

    ```bash
    top
    ```

50. **List logged-in users with headers:**

    ```bash
    w
    ```

---

## ✅ Bonus Challenge Solution

**Script: `devops_practice.sh`**

```bash
#!/bin/bash

# Create directory and files
mkdir -p practice_dir
cd practice_dir
touch a.txt b.txt c.txt

# Set ACL
setfacl -m u:testuser:rwx a.txt b.txt c.txt

# Show disk & memory usage
free -h | head -n 2
df -h | grep '^/dev'

# Find all .sh files modified today
find /home -type f -name "*.sh" -mtime 0
```

Make script executable:

```bash
chmod +x devops_practice.sh
./devops_practice.sh
```

---

### ✍️ Author

**Ophid**
*DevOps & Backend Engineer – Linux | Cloud | Automation*
