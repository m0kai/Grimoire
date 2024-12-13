-- -
### General Usage
`(Pwn3d!)` signifies you can login and use system commands, usually also means local admin. 
```bash
# works the same way independent of protocol
# you can put a single username or password
# or you can put a list for bruteforcing either using the same flags
# -u: username or user list
# -p: password or password list
netexec <protocol> <ip> -u <username or user list> -p <password or password list>
netexec smb 10.10.10.10 -u jack -p Password123
netexec winrm 10.10.10.10 -u user.lst -p rockyou.txt

# continue attack even if a valid login is found
netexec winrm 10.10.10.10 -u user.lst -p rockyou.txt --continue-on-success
```
### SMB
```bash
# list available shares for a given user
netexec smb <ip> -u <username> -p <passwd> --shares
```
### Password Spray
```bash
# local auth
netexec <protocol> <ip> -u <userlist> -p '<passwd>' --local-auth 

# AD
netexec <protocol> <ip> -u <userlist> -p '<passwd>'
```
### PsExec
![[Dark Arts I/Services/SMB/Tools/PSExec#^2f3c64|PSExec]]
### Enum Logged on Users
If you have local admin access, you can see which users are currently logged into the system.
```bash
netexec smmb <ip> -u <user> -p '<passwd>' --loggedon-users
```