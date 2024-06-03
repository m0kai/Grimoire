-- -
Can be used outside of an AD context but generally used in an AD context. 
#### Enumerating AD Password Policy
Requires you have valid credentials first.
```bash
crackmapexec smb <ip> -u <user> -p <passwd> --pass-pol
crackmapexec smb 172.16.5.5 -u avazquez -p Password123 --pass-pol
```

^016942

#### Enumerating valid domain users w/o credentials
```bash
crackmapexec smb <dc ip> --users
crackmapexec smb 172.16.5.5 --users
```

^99029f
