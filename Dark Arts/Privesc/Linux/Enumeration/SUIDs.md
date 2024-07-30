-- -
Look for software with the SUID bit set so that they always run with root privileges. Of course, not all programs with the SUID bit set are vulnerable, but you may find a vulnerable program.
#### Find
Use the find command to pull out all programs on the filesystem with the SUID bit set:
```bash
find / -perm -u=s -type f 2>/dev/null
find / -type f -perm -04000 -ls 2>/dev/null
```

^ed7f08

From here, quickest wins are to search the programs output here using [GTFOBins](https://gtfobins.github.io/#+suid)
Otherwise, check your [[Abuse SUIDs|SUID Exploit Notes]].

#### Share Object Injection
#SOInjection Something to do when you find strange SUID programs with no GTFOBins entry and you want to see if you can toy with it to hijack it. 
#### Enum
```bash
# do the find above to find SUID programs
# find one that looks custom or weird and isn't coming up on GTFO bins
# try to derive what it does by running it. In the example it's a program:
# /usr/local/bin/suid-so
/usr/local/bin/suid-so

# if you can't get anything from just running it, then use strace to have it spit out what it's doing under the hood
strace /usr/local/bin/suid-so 2>&1 # general
strace /usr/local/bin/suid-so 2>&1 | grep -i -E "open|access|no such file" 

# In the output, you are looking for something along the lines of:
# No such file or directory

# This is an injection point where you may be able to hijack execution and redirecct it to do something you want it to do, like get a shell or read a privileged file. 

# Of course, you are looking for a file you can access/replace/write so you are looking for something in a user directory or a tmp directory or any directory you have access to write to a file. 
```

^8b428f

[[Abuse SUIDs#^2ec112|Exploit]]

#### CVE-2016-1247

^14400b

#cve-2016-1247 [Explanation](https://legalhackers.com/advisories/Nginx-Exploit-Deb-Root-PrivEsc-CVE-2016-1247.html), If certain conditions are met, a user www-data is able to escalate privileges to root. 
##### Conditions:
1. You are `www-data`
2. System is Debian-based (debiand, ubuntu, etc)
3. nginx version `< 1.6.2` is on the server
##### Enum
```bash
# Verify your are www-data
whoami

# automated
./linux-exploit-suggester.sh

# output will likely be various, but we are looking for
# [CVE-2016-1247] nginxed-root.sh

# manually check nginx version
dpkg -l | grep nginx

# should output version:
# 1.6.2 or less

# make sure sudo has the SUID bit set:
find / -type f -perm -04000 -ls 2>/dev/null

# Verify logs exist and you own /var/log/nginx
ls -la /var/log/nginx

# output should show something like:
# drwxr-x--- 2 www-data adm 4096 Jun 16 06:25 .
# this shows rwx for owner and shows www-data as owner
```

#### Env Variables
This is a specific vector, you look through the SUID software and look for custom programs or weird programs you may be able to manipulate. The key point here is to look for software that is run by the SUID porgram that you maybe can replace with your own program to get a shell. 
```bash
# as above, dump SUID files:
find / -perm -u=s -type f 2>/dev/null

# for this example, lets say you found:
# /usr/local/bin/suid-env
# Run it to see what it does
/usr/local/bin/suid-env

# if that doesn't give you any immediate ideas, pass it through strings
strings /usr/local/bin/suid-env

# from here there are two examples to highlight:
# 1) no absolute paths used
# output of strings reveals:
# service apache2 start

# 2) absolute path is used:
# output of strings reveals:
# /usr/sbin/service apach2 start
```
From here, [[Abuse SUIDs#^460797|Exploit]]