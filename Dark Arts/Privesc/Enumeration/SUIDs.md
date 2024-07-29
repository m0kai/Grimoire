-- -
Look for software with the SUID bit set so that they always run with root privileges. Of course, not all programs with the SUID bit set are vulnerable, but you may find a vulnerable program.
#### Find
Use the find command to pull out all programs on the filesystem with the SUID bit set:
```bash
find / -perm -u=s -type f 2>/dev/null
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
