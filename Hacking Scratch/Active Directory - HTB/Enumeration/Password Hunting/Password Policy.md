-- -
If you have a foothold on AD i.e. you have a valid set of credentials for an AD account with any level of access, you can use that account to enumerate the password policy and help you stay within the lockout policy bounds to conduct a [[Hacking Scratch/Active Directory - HTB/Attacks/Password Spray]] attack. 

If you don't have a foothold/valid credentials, you can try to leverage an SMB NULL session or LDAP anonymous bind to enumerate the password policy using [[rpcclient]].

### From Linux
#### rpcclient (w/o valid creds)
![[rpcclient#^c2a0e3]]
#### enum4linux (w/o valid creds)
Vanilla enum4linux
![[enum4linux#^43abe2]]
enum4linux next gen (enum4linux-ng)
![[enum4linux#^68bcee]]
#### ldapsearch (w/o valid creds)
```bash
ldapsearch -h <ip> -x -b "DC=<dc name>,DC=<domain>" -s sub "*" | grep -m 1 -B 10 pwdHistoryLength

ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "*" | grep -m 1 -B 10 pwdHistoryLength
```
#### crackmapexec (with valid creds)
![[Hacking Scratch/Tools/Active Directory/Linux/crackmapexec#^016942]]
### From Windows
#### net binary
```powershell
net use \\DC01\ipc$ "" /u:""
net use \\DC01\ipc$ "" /u:guest
net accounts
```
#### PowerView
![[PowerView (depricated)#^b29806]]