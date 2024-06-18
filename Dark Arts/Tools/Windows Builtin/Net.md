-- -
#### User Account Enum
```powershell
# Info on password requirements
net accounts

# Password and Lockout Policy
net accounts /domain

# List all users of the domain
net user /domain 

# Info on current user
net user %username%
```

^b53466

#### Domain Group Enum
```powershell
# info on domain groups
net group /domain

# List users w/ domain admin privs
net group "Domain Admins" /domain

# List domain groups
net groups /domain

# list users that belong to the administrators group inside the domain.
# Domain Admins are included here by default
net localgroup administrators /domain
```

^73bbfb

#### Local Group Enum
```powershell
# list available groups
net localgroup

# info on admin group
net localgroup Administrators

# Add user to administrators group
net localgroup administrators <username> /add 
```

^f80f3a

#### Share Enum
```powershell
# Check current shares
net share

# View shares on the domain
net view /all /domain[:domainname]

# list shares of a computer
net view /computer /ALL 

# mount share locally
net use x: \computer\share
```

^a64810

#### Computers enum
```powershell
# List PCs connected to domain
net group "domain computers" /domain

# List PC accounts of Domain Controllers
net group "Domain Controllers" /domain

# List PCs of the domain
net view /domain
```

^b574e9
