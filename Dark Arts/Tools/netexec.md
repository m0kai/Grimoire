-- -
### General Usage
`(Pwn3d!)` signifies you can login and use system commands, usually also means local admin. 
```bash
# works the same way independent of protocol
# you can put a single username or password
# or you can put a list for bruteforcing either using the same flags
# -u: username or user list
# -p: password or password list
netexec <protocol> -u <username or user list> -p <password or password list>
netexec smb -u jack -p Password123
netexec winrm -u user.lst -p rockyou.txt
```
### SMB
```bash
# list available shares for a given user
netexec smb <ip> -u <username> -p <passwd> --shares
```