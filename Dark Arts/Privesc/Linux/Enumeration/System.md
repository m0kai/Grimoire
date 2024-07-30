-- -
Orient yourself onto what type of system you are on. 
#### Build Info
Use this info to search for [[Kernel Exploits]]
```bash
# Kernel version
uname -a
cat /proc/version

# Distro version
cat /etc/issue

# Architecture
lscpu
```
#### Process Info
```bash
# All
ps aux

# by user
ps aux | grep <user>
ps aux | grep root
```
#### Search for Kernel Level Exploits
```bash
# ---- Manual ----
# as above
uname -a 

# Let say that output:
# Linux debian 2.6.32-5amd64
Linux debian 2.6.32-5-amd64 exploit # type into google
searchsploit Linux debian 2.6.32-5amd64 # search exploitDB locally

# metasploit
msfconosle
search Linux debian 2.6.32-5amd64

# For above version, system could be vulnerable to Dirty Cow

# ---- Automated ----
./linux-exploit-suggestor

```

^c36ae3
