# DEVOPS 3

# Linux And Shell Scripting

* In this lecture we are going to learn about following topics -:

1. user
2. usergroups
3. sudo
4. grep
5. awk
6. ACL (Access Control List)
7. ssh (secure Shell), scp (sever Copy)
8. system ctc

---

### User Management

-> First let's create a new user -:

```bash
aditya@MORK:/mnt/h/MORK/adityaubantu$ whoami
aditya
aditya@MORK:/mnt/h/MORK/adityaubantu$ useradd ayush-dev -m
useradd: Permission denied.
useradd: cannot lock /etc/passwd; try again later.
```

so I tried to create a new user by using the command `useradd user_name -m(manage)`

* `" -m"` -> here `-m` is a flag which creates a `/home/userName_Directory` directory for the new user is created

* but as I am a normal user I cant add new user and I get a warning of permission denied which is :
  `cannot lock /etc/passwd; try again later.`

* here `/etc/passwd` : is a file which contain all the user's information

* for creation of new user we should be a superuser (rootuser)

//below is the command for creation of new user and reading the content of the `/etc/passwd/` file

```bash
aditya@MORK:/mnt/h/MORK/adityaubantu$ sudo useradd ayush-dev -m
[sudo] password for aditya:
aditya@MORK:/mnt/h/MORK/adityaubantu$ sudo cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
_apt:x:42:65534::/nonexistent:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:998:998:systemd Network Management:/:/usr/sbin/nologin
systemd-timesync:x:996:996:systemd Time Synchronization:/:/usr/sbin/nologin
dhcpcd:x:100:65534:DHCP Client Daemon,,,:/usr/lib/dhcpcd:/bin/false
messagebus:x:101:101::/nonexistent:/usr/sbin/nologin
syslog:x:102:102::/nonexistent:/usr/sbin/nologin
systemd-resolve:x:991:991:systemd Resolver:/:/usr/sbin/nologin
uuidd:x:103:103::/run/uuidd:/usr/sbin/nologin
landscape:x:104:105::/var/lib/landscape:/usr/sbin/nologin
polkitd:x:990:990:User for polkitd:/:/usr/sbin/nologin
aditya:x:1000:1000:,,,:/home/aditya:/bin/bash
ayush-dev:x:1001:1001::/home/ayush-dev:/bin/sh
aditya@MORK:/mnt/h/MORK/adityaubantu$
```

* as we can see in the `/etc/passwd` file contain the information of all the users available in this machine.

* Now I have created a new user but it does not have it's password so let's set his password for that we should be a superuser.

```bash
aditya@MORK:/mnt/h/MORK/adityaubantu$ sudo passwd ayush-dev
New password: ayushuser
Retype new password:
passwd: password updated successfully
aditya@MORK:/mnt/h/MORK/adityaubantu$
```

// now trying to go `/home/ayush-dev/`

```bash
aditya@MORK:/$ cd /home/ayush-dev
-bash: cd: /home/ayush-dev: Permission denied
```

-> but we get the permission denied because can't just go inside other users house/home
-> this is kind of security linux /ubantu is providing us

//now let's swith the user to ayush-dev using "su" command

```bash
aditya@MORK:/$ whoami
aditya
aditya@MORK:/$ su ayush-dev
Password:
$ whoami
ayush-dev
$ cd /home/ayush-dev
$ pwd
/home/ayush-dev
$ mkdir dev_files
$ pwd
/home/ayush-dev
$ cd dev_files
$ pwd
/home/ayush-dev/dev_files
$ touch dev_file.txt
$ ls
dev_file.txt
$ exit
aditya@MORK:/$ whoami
aditya
aditya@MORK:/$
```

-> as you can se in the above commands I am a user `aditya` then swith to the `ayush-dev` user and when I run command `exit` I come back to the `aditya` user because this how the user management work in the linux
-> so if you start your machine and you login first using the any user and then swith to different  user and if you do `exit` you will back to the nomral user which you initily get loggedin in you machine.

// Now tet's create some users

```bash
aditya@MORK:/$ sudo useradd aditya-dev
aditya@MORK:/$ sudo passwd aditya-dev
New password:
Retype new password:
Sorry, passwords do not match.
passwd: Authentication token manipulation error
passwd: password unchanged
aditya@MORK:/$ sudo useradd aditya-tester
aditya@MORK:/$ sudo passwd aditya-tester
New password:
Retype new password:
passwd: password updated successfully
aditya@MORK:/$ sudo useradd aditya-devops
aditya@MORK:/$ sudo passwd aditya-devops
New password:
Retype new password:
passwd: password updated successfully
```

-> the file where I can get the infomoration that how many users we have created or how many users exists in this machine run commmand `sudo cat /etc/passwd/ ` in this file last you will get.

```bash
aditya@MORK:/$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/run/ircd:/usr/sbin/nologin
_apt:x:42:65534::/nonexistent:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
systemd-network:x:998:998:systemd Network Management:/:/usr/sbin/nologin
systemd-timesync:x:996:996:systemd Time Synchronization:/:/usr/sbin/nologin
dhcpcd:x:100:65534:DHCP Client Daemon,,,:/usr/lib/dhcpcd:/bin/false
messagebus:x:101:101::/nonexistent:/usr/sbin/nologin
syslog:x:102:102::/nonexistent:/usr/sbin/nologin
systemd-resolve:x:991:991:systemd Resolver:/:/usr/sbin/nologin
uuidd:x:103:103::/run/uuidd:/usr/sbin/nologin
landscape:x:104:105::/var/lib/landscape:/usr/sbin/nologin
polkitd:x:990:990:User for polkitd:/:/usr/sbin/nologin
aditya:x:1000:1000:,,,:/home/aditya:/bin/bash
ayush-dev:x:1001:1001::/home/ayush-dev:/bin/sh
aditya-dev:x:1002:1002::/home/aditya-dev:/bin/sh
aditya-tester:x:1003:1003::/home/aditya-tester:/bin/sh
aditya-devops:x:1004:1004::/home/aditya-devops:/bin/sh
aditya@MORK:/$
```

-> as we can see all the user's at the last of this file

//Now let's create the devops group
-> `sudo groupadd devops`

* to check weather the group is created or not you should go to the `sudo cat /etc/group/` in the last of this file you will get all the groups
* and you will also find that all the user's we created and also we as defulat user is also their as a group
* so linux treated all the users as a groups

```bash
aditya@MORK:/$ groupadd devops
groupadd: Permission denied.
groupadd: cannot lock /etc/group; try again later.
aditya@MORK:/$ sudo groupadd devops
aditya@MORK:/$ sudo cat /etc/group
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:syslog,aditya
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:
fax:x:21:
voice:x:22:
cdrom:x:24:aditya
floppy:x:25:
tape:x:26:
sudo:x:27:aditya
audio:x:29:
dip:x:30:aditya
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
shadow:x:42:
utmp:x:43:
video:x:44:
sasl:x:45:
plugdev:x:46:aditya
staff:x:50:
games:x:60:
users:x:100:aditya
nogroup:x:65534:
systemd-journal:x:999:
systemd-network:x:998:
crontab:x:997:
systemd-timesync:x:996:
input:x:995:
sgx:x:994:
kvm:x:993:
render:x:992:
messagebus:x:101:
syslog:x:102:
systemd-resolve:x:991:
uuidd:x:103:
_ssh:x:104:
landscape:x:105:
polkitd:x:990:
admin:x:106:
netdev:x:107:
aditya:x:1000:
ayush-dev:x:1001:
aditya-dev:x:1002:
aditya-tester:x:1003:
aditya-devops:x:1004:
devops:x:1005:
aditya@MORK:/$
```

->so as you can see the groups at the last of this file

//Now let's add a single user in a devops group first

* for that running a command `"sudo gpasswd -a userName groupName"`

* `gpsswd` -> is a command which pass (allowed) us to add user in any group

* `"-a"` means standalone (means adding a alone(single) user in a group means appending the user one by one.

* `"-M"` -> if used means add/overwrites multiple users in the group.

`aditya@MORK:/$ sudo gpasswd -a aditya-dev devops
Adding user aditya-dev to group devops`
-this iis the commmand which I run

// Now how to confirm that aditya-dev added to group devops or not again check the content of file `/etc/group` file

```bash
aditya@MORK:/$ sudo cat /etc/group
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:syslog,aditya
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:
fax:x:21:
voice:x:22:
cdrom:x:24:aditya
floppy:x:25:
tape:x:26:
sudo:x:27:aditya
audio:x:29:
dip:x:30:aditya
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
shadow:x:42:
utmp:x:43:
video:x:44:
sasl:x:45:
plugdev:x:46:aditya
staff:x:50:
games:x:60:
users:x:100:aditya
nogroup:x:65534:
systemd-journal:x:999:
systemd-network:x:998:
crontab:x:997:
systemd-timesync:x:996:
input:x:995:
sgx:x:994:
kvm:x:993:
render:x:992:
messagebus:x:101:
syslog:x:102:
systemd-resolve:x:991:
uuidd:x:103:
_ssh:x:104:
landscape:x:105:
polkitd:x:990:
admin:x:106:
netdev:x:107:
aditya:x:1000:
ayush-dev:x:1001:
aditya-dev:x:1002:
aditya-tester:x:1003:
aditya-devops:x:1004:
devops:x:1005:aditya-dev

- now as you can see that devops group after the colon it contain aditya-dev
```

//now adding mutliple user in a group at a time by usig the -M option but this will overrites our group memebers

```bash
aditya@MORK:/$ sudo gpasswd -M aditya-devops,ayush-dev devops
aditya@MORK:/$ sudo cat /etc/group
root:x:0:
daemon:x:1:
bin:x:2:
sys:x:3:
adm:x:4:syslog,aditya
tty:x:5:
disk:x:6:
lp:x:7:
mail:x:8:
news:x:9:
uucp:x:10:
man:x:12:
proxy:x:13:
kmem:x:15:
dialout:x:20:
fax:x:21:
voice:x:22:
cdrom:x:24:aditya
floppy:x:25:
tape:x:26:
sudo:x:27:aditya
audio:x:29:
dip:x:30:aditya
www-data:x:33:
backup:x:34:
operator:x:37:
list:x:38:
irc:x:39:
src:x:40:
shadow:x:42:
utmp:x:43:
video:x:44:
sasl:x:45:
plugdev:x:46:aditya
staff:x:50:
games:x:60:
users:x:100:aditya
nogroup:x:65534:
systemd-journal:x:999:
systemd-network:x:998:
crontab:x:997:
systemd-timesync:x:996:
input:x:995:
sgx:x:994:
kvm:x:993:
render:x:992:
messagebus:x:101:
syslog:x:102:
systemd-resolve:x:991:
uuidd:x:103:
_ssh:x:104:
landscape:x:105:
polkitd:x:990:
admin:x:106:
netdev:x:107:
aditya:x:1000:
ayush-dev:x:1001:
aditya-dev:x:1002:
aditya-tester:x:1003:
aditya-devops:x:1004:
devops:x:1005:aditya-devops,ayush-dev
```

-> see as you can see aditya-devops and ayush-dev is added but aditya-dev get overrite so remember while using the -M you can loss your members of gruop so add those users also while using the -M command

* `" sudo gpasswd -M aditya-dev,ayush-dev,aditya-devops devops"`

* now added all the users.

```bash
$ sudo gpasswd -a aditya devops
Adding user aditya to group devops
```

* added aditya also and `-a` will not loss the members because it appends the user.

\###Note

* `devops:x:1005:aditya-dev,ayush-dev,aditya-devops,aditya`
* For now what we have done created a group of devops and added  4 memebers in it
* but for now one user can't access the another user home directory because it's his/her personal things may be their
* So? how can a user access the home of another user?Is theire a way?
* Yeas! That's why we create a group of 4 members and groups are created to share the things
* So, if I'll give "all" persmision to the devops group so now all the memebers of group can acess all the things of another members home, but this is not good may be a user may have some persnal files overtheir in his or her home so for that we just give the persmission of a certain file or folder to the group so that memebers can access other memebers those things only which should be shared not all things.

### Now let's talk about the sudo what is this? from where it is comming?

-> so go and read the content of a file "/etc/sudoers" open it in a editor (vim)

-> sudoers - is a configuration file in which all ther config regarding the all permision of a system is present

* So After opening this file go in the last you will find -:

```
# User privilege specification
root    ALL=(ALL:ALL) ALL

# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
```

* the above thing is the last content of the `/etc/sudoers` file

* so as you can see root user, or superuser has all ther permission of system is set or giving in this file

* and can you see the `%sudo` which is a group and also all ther system permission is given to this group
  and also writen above that -:
  `"#Allow members of group sudo to execute any command"`

* So, Now I understands that sudo is a group which has all the system permissions

* And also we understand that `/etc/sudoers` is configuration file from where we can give all the permission to any group or user  at once. How I know this ?? because mention in the file I attached below

```
# Host alias specification

# User alias specification

# Cmnd alias specification

# User privilege specification
```

### adding our devops folder in /etc/sudoers file

* as we know that for now our devops memebers users does not have permission to go another members home directory inside

* to add the group in the /etc/sudoers file open it in vim editor or any

* then add group and can give all the permission

Example -:

```
# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL
%devops All = (All) All
```

* `%` -> to show that this is a group
* `devops` -> name of group
* 1. `ALL` ->mai devops group ko saari permission de raha hun ese ki...
* 2. `(ALL)` -> ...devops group All users ko access kr pay...
* 3. `ALL` -> ...ki wo saary users ke folders ko access kr sakke.

then press `Esc + : + wq! + Enter` to overrites the content of the `/etc/sudoers` file
and then run command  `reboot` or `sudo reboot` this will reboot your all the permission .

// Changing the permision of the file

```bash
aditya@MORK:/home/aditya-dev$ cd dev_files && ls
dev_file.txt
aditya@MORK:/home/aditya-dev/dev_files$
```

* now as you can see their is a file in a aditya-dev user I want to change the permission of that file for the User,groups,other-Users

* for that you have to use a command change mode which is `"sudo chmod user_number group_number otherUser_number"`

* their is a table for numbers which are assign to the read+write+execute permission

```bash
aditya@MORK:/home/aditya-dev/dev_files$ ls -la
total 8
drwxrwxr-x 2 aditya-dev aditya-dev 4096 Sep 18 03:16 .
drwxr-xr-x 3 aditya-dev aditya-dev 4096 Sep 18 03:15 ..
-rw-rw-r-- 1 aditya-dev aditya-dev    0 Sep 18 03:16 dev_file.txt
aditya@MORK:/home/aditya-dev/dev_files$
```

-see the cureent permission of the  dev\_files
`-rw - for user`
`- rw - for group`
`- r - for other users`

now chagning and giving full permissions to all

```bash
 aditya@MORK:/home/aditya-dev/dev_files$ sudo su aditya-dev
$ pwd
/home/aditya-dev/dev_files
$ ls-la
sh: 2: ls-la: not found
$ ls -la
total 8
drwxrwxr-x 2 aditya-dev aditya-dev 4096 Sep 18 03:16 .
drwxr-xr-x 3 aditya-dev aditya-dev 4096 Sep 18 03:15 ..
-rwxrwxrwx 1 aditya-dev aditya-dev    0 Sep 18 03:16 dev_file.txt
$ chmod 700 dev_file.txt
$ ls -la
total 8
drwxrwxr-x 2 aditya-dev aditya-dev 4096 Sep 18 03:16 .
drwxr-xr-x 3 aditya-dev aditya-dev 4096 Sep 18 03:15 ..
-rwx------ 1 aditya-dev aditya-dev    0 Sep 18 03:16 dev_file.txt

$ chmod 750 dev_file.txt
$ ls -la
total 8
drwxrwxr-x 2 aditya-dev aditya-dev 4096 Sep 18 03:16 .
drwxr-xr-x 3 aditya-dev aditya-dev 4096 Sep 18 03:15 ..
-rwxr-x--- 1 aditya-dev aditya-dev    0 Sep 18 03:16 dev_file.txt
$
```

* at the end aditya-dev user change the permission of `dev_file.txt` to -:
  user-> read+write+execute = 7
  group-> read+exectue = 5
  other-users -> no permission = 0

## note remember whenever you are changing any permission of folder group or file you should do reboot `"sudo reboot"`

// Now time to learn the ACL (Access Control List)

* to use this you have to install this first fromt he internet so -> `"sudo apt-get install acl"`

ACL (Access Control Lists) in Linux is not an external package you download from the internet, it’s actually a feature built into the Linux kernel and supported by most modern filesystems (like ext4, xfs, btrfs, etc.).

Here’s the breakdown:

🔹 Traditional Permission Model

Works with owner, group, and others.

Limited: you can only assign permissions to one owner and one group.

🔹 ACL (Access Control List)

Extends that model.

Lets you give specific users or groups custom permissions on a file/directory.

Much more flexible — e.g.,

Allow user A to only read a file.

Allow user B to both read and write.

Allow group C to execute it.

//Now using the ACL and getting the permmision infomration of a file for that you have to use a command which is -:

* `"getfacl"` -> get file acess control list means permission

```bash
aditya@MORK:/home/aditya-dev/dev_files$ sudo getfacl /home/aditya-dev/dev_files/dev_file.txt
getfacl: Removing leading '/' from absolute path names
# file: home/aditya-dev/dev_files/dev_file.txt
# owner: aditya-dev
# group: aditya-dev
user::rwx
group::r-x
other::---
```

\--> see as you can see how the permission are shown in good manner

//now using the ACL we can also give permission to perticular user to a perticular file by using the command -> `"setfacl -m u:user_name:rwx(permissions) /filelocation/file.txt"`

```bash
aditya@MORK:/$ # Let's give aditya user rwe permission of file dev_file.txt
aditya@MORK:/$ sudo setfacl -m u:aditya:rwx /home/aditya-dev/dev_files/dev_file.txt
aditya@MORK:/$ sudo getfacl /home/aditya-dev/dev_files/dev_file.txt
getfacl: Removing leading '/' from absolute path names
# file: home/aditya-dev/dev_files/dev_file.txt
# owner: aditya-dev
# group: aditya-dev
user::rwx
user:aditya:rwx
group::r-x
mask::rwx
other::---
```

* in above commands I have given the permission user aditya of rwx for the file dev\_file.txt and as we can see the permissions of the file their is mention of  `user:aditya:rwx` permissions.

```bash
aditya@MORK:/$ whoami
aditya
aditya@MORK:/$ echo "user Aditya is wrting in the file dev_file.txt : Namaste file " > /home/aditya-dev/dev_files/dev_file.txt
aditya@MORK:/$ cat /home/aditya-dev/dev_files/dev_file.txt
user Aditya is wrting in the file dev_file.txt : Namaste file
aditya@MORK:/$
```

* in the above commands as you can see that user aditya can write and read the content of the file dev\_files.txt

\---> I simple way ACL make easy to get and set the permissions

-> their are 2 important commands in the ACL getfacl and setfacl

* getfacl -> get the permission of a file
* setfacl -> set the permission of a file
* so ACL allow you to give specefic permission without the changing of the ownership

### Now let's learn about the GREP(global Regular Expression Print) "grep" comand

* this command is used to search a perticular string or pattern in a file or multiple files and return you a list which contain that search thing.

* to serch all the files in the folder you have to search recersivly so use `"grep -r Search_String_or_Error /folderName"`

* For searching in a perticular file `"grep Search_String_or_error /fileName.extention"`

```bash
aditya@MORK:/$ grep -r devops /home
grep: /home/ayush-dev: Permission denied
/home/aditya/.bash_history:sudo useradd aditya-devops
/home/aditya/.bash_history:sudo passwd aditya-devops
/home/aditya/.bash_history:groupadd devops
/home/aditya/.bash_history:sudo groupadd devops
/home/aditya/.bash_history:sudo gpasswd aditya-dev devops
/home/aditya/.bash_history:sudo passwd -a aditya-dev devops
/home/aditya/.bash_history:sudo gpasswd -a aditya-dev devops
/home/aditya/.bash_history:sudo gpasswd -m ayush-dev aditya-devops devops
/home/aditya/.bash_history:sudo gpasswd -m ayush-dev, aditya-devops devops
/home/aditya/.bash_history:sudo gpasswd -M aditya-devops ayush-dev devopos
/home/aditya/.bash_history:sudo gpasswd -M aditya-devops,ayush-dev devopos
/home/aditya/.bash_history:sudo gpasswd -M aditya-devops,ayush-dev devops
/home/aditya/.bash_history:sudo gpasswd -M aditya-dev, ayush-dev, aditya-devops devops
/home/aditya/.bash_history:sudo gpasswd -M aditya-dev,ayush-dev,aditya-devops devops
/home/aditya/.bash_history:sudo gpasswd -a aditya devops
/home/aditya/.bash_history:sudo mkdir /home/aditya-devops
/home/aditya/.bash_history:sudo chown aditya-devops:aditya-devops /home/aditya-devops
/home/aditya/.bash_history:sudo chmod 755 /home/aditya-devops
/home/aditya-dev/dev_files/dev_file.txt:devops
aditya@MORK:/$ grep devops /home/aditya-dev/dev_files/dev_file.txt
devops
aditya@MORK:/$ grep -r devops /home/aditya-dev/dev_files
/home/aditya-dev/dev_files/dev_file.txt:devops
aditya@MORK:/$
```

/// above is the command of useing grep but for now we are just searching the case sensetive data means only what is typed for the searching that string or rqular expression will be found

* but what If I want to search case insensetive data
* for that just use `"-i "` insensetive option in the grep command

Example -:

```bash
aditya@MORK:/$ grep -r -i devops /home/aditya-dev/dev_files
/home/aditya-dev/dev_files/dev_file.txt:DevOps
/home/aditya-dev/dev_files/dev_file.txt:devops

see -> I search for devops I get both devops and DevOps also because now using "-i"
```

-> you can also search like - I want to find word's which contain word "t" then search `"grep -ir t* /folder"` - remeber -ir is same as -r and -i vise versa

Example -:

```bash
aditya@MORK:/mnt/h/MORK/adityaubantu$ grep -ri t* /home/aditya-dev
/home/aditya-dev/dev_files/dev_file.txt:user Aditya is wrting in the file dev_file.txt : Namaste file
/home/aditya-dev/dev_files/dev_file.txt:
/home/aditya-dev/dev_files/dev_file.txt:DevOps
/home/aditya-dev/dev_files/dev_file.txt:
/home/aditya-dev/dev_files/dev_file.txt:devops
```

* A question that if you have to confirm that the user is created is confirmed or not ?
* solition -> grep the userName in the `/etc/passwd` file

```bash
 aditya@MORK:/mnt/h/MORK/adityaubantu$ sudo grep aditya-dev /etc/passwd
[sudo] password for aditya:
aditya-dev:x:1002:1002::/home/aditya-dev:/bin/sh
aditya-devops:x:1004:1004::/home/aditya-devops:/bin/sh
```

### Now the "find" command

-> find command is also important in the linux which is used to find the files based on some conditon
Example -> find a file which has 777 permission
etc...

### Log file

* Log file in linux is a file which contain all the system log information like when system started when ends any other application running , error informations.

* Why we are talking about the log file because log file is what devops Engineer used a lot and check and search over their

* So, we can use grep,find but their is another command which more powerfull compare to to them that is awk.

### awk command

-> awk commmand is used to search, filter out specefic data based on query like  a programming language
or
-> awk is a command-line tool and a small programming language in Unix/Linux, designed for text processing. It scans files line by line, searches for patterns, splits data into fields, and lets you perform actions like printing, filtering, and formatting.

* format -:
* `awk ' /SearchingWord/ {print NR $col1, $col2, $coln}' fileName.txt`
* `NR` -> number of Rows - give number of rows that where the perticular text encounters.

// below is the command for searching the Error word in the log\_file.txt and printing Number of rows with col1, col2, col4

```bash
aditya@MORK:/mnt/h/MORK/adityaubantu$ awk '/ERROR/ {print NR,$1,$2,$4}' log_file.txt
2 2025-09-18 10:00:05 (pid
5 2025-09-18 10:00:20 (pid
7 2025-09-18 10:00:30 (pid
10 2025-09-18 10:00:45 (pid
13 2025-09-18 10:01:00 (pid
16 2025-09-18 10:01:15 (pid
20 2025-09-18 10:01:35 (pid
23 2025-09-18 10:01:50 (pid
26 2025-09-18 10:02:05 (pid
30 2025-09-18 10:02:25 (pid
33 2025-09-18 10:02:40 (pid
36 2025-09-18 10:02:55 (pid
39 2025-09-18 10:03:10 (pid
43 2025-09-18 10:03:30 (pid
46 2025-09-18 10:03:45 (pid
49 2025-09-18 10:04:00 (pid
52 2025-09-18 10:04:15 (pid
55 2025-09-18 10:04:30 (pid
58 2025-09-18 10:04:45 (pid
61 2025-09-18 10:05:00 (pid
64 2025-09-18 10:05:15 (pid
67 2025-09-18 10:05:30 (pid
71 2025-09-18 10:05:50 (pid
74 2025-09-18 10:06:05 (pid
77 2025-09-18 10:06:20 (pid
80 2025-09-18 10:06:35 (pid
83 2025-09-18 10:06:50 (pid
86 2025-09-18 10:07:05 (pid
89 2025-09-18 10:07:20 (pid
92 2025-09-18 10:07:35 (pid
95 2025-09-18 10:07:50 (pid
```

//Now suppose I want to just get the Number of row of ERROR from 1 to 10 only means NR>1 && NR<10
then the command will be -:

```bash
'aditya@MORK:/mnt/h/MORK/adityaubantu$ awk 'NR>1 && NR<10 && /ERROR/ {print NR}' log_file.txt
2
5
7
'
```

* one more example with the specefic column getting

```bash
aditya@MORK:/mnt/h/MORK/adityaubantu$ awk 'NR>1 && NR<20 && /ERROR/ {print NR,$1,$3,$4}' log_file.txt
2 2025-09-18 [ERROR] (pid
5 2025-09-18 [ERROR] (pid
7 2025-09-18 [ERROR] (pid
10 2025-09-18 [ERROR] (pid
13 2025-09-18 [ERROR] (pid
16 2025-09-18 [ERROR] (pid
```

//BElow is the good example of && operator

```bash
aditya@MORK:/mnt/h/MORK/adityaubantu$ touch Error_upto_50.txt && awk 'NR>0 && NR<51 && /ERROR/ {print NR,$1,$2,$4,$5,$6}' log_file.txt > Error_upto_50.txt
aditya@MORK:/mnt/h/MORK/adityaubantu$ ls
Error_upto_50.txt  log_file.txt
aditya@MORK:/mnt/h/MORK/adityaubantu$ cat Error_upto_50.txt
2 2025-09-18 10:00:05 (pid 9876): File
5 2025-09-18 10:00:20 (pid 3456): Connection
7 2025-09-18 10:00:30 (pid 1122): Database
10 2025-09-18 10:00:45 (pid 5544): Permission
13 2025-09-18 10:01:00 (pid 6677): Request
16 2025-09-18 10:01:15 (pid 4455): File
20 2025-09-18 10:01:35 (pid 1357): Authentication
23 2025-09-18 10:01:50 (pid 6420): Permission
26 2025-09-18 10:02:05 (pid 3097): Connection
30 2025-09-18 10:02:25 (pid 6497): File
33 2025-09-18 10:02:40 (pid 3164): Database
36 2025-09-18 10:02:55 (pid 2831): Permission
39 2025-09-18 10:03:10 (pid 5498): Request
43 2025-09-18 10:03:30 (pid 9054): File
46 2025-09-18 10:03:45 (pid 2721): Database
49 2025-09-18 10:04:00 (pid 5488): Aut
```

---

### SSH & SCP (repeat of original SCP examples)

**SCP upload example (as provided earlier):**

```bash
scp -i client-key-file.pem file_name.txt server_name : folder_location_on_server/where_to_put_file
```

**SCP download example (as provided earlier):**

```bash
scp -i client-key-file.pem server_name : folder_location_of_server/file.txt  client_folder_location/where_to_put_file
```

---

## Notes / Reminders from lecture (verbatim important points):

* `-m` flag -> creates /home/userName\_Directory directory for the new user is created
* `/etc/passwd` file contain the information of all the users available in this machine.
* for creation of new user we should be a superuser (rootuser)
* `gpasswd -a` -> append single user to group
* `gpasswd -M` -> overwrite group members (be careful, you can lose previous members)
* `sudoers` file controls user/group sudo privileges
* `%` before a name in sudoers means it is a group (example: `%devops`)
* Permission numbers: read = 4, write = 2, execute = 1
* Use `chmod` with numeric codes to set permissions (e.g. `chmod 750 file.txt`)
* Use `getfacl` and `setfacl` to get/set ACLs
* Use `grep` (and `-r`, `-i`) to search files and directories
* Use `awk` to scan and process log files (`NR`, `$1`, `$2`, etc.)
* Log files live in `/var/log` and are essential for debugging and monitoring

---

