-- -
Command you keep looking up every single time you are trying to get privesc on linux
#### Find SUID binaries
```bash
find / -perm -u=s -type f 2>/dev/null
```