-- -
Orient yourself onto what type of system you are on. 
#### Build Info
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