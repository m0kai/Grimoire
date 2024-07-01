-- -
PowerShell has an Active Directory Module for administering an AD environment, depending on the level of access you have, and if you have access to PowerShell on the AD environment, you can enumerate AD directly from PowerShell. Given my experience, you should have access to at least some of this given valid credentials. #stealthy method of enumerating this data as it will allow our traffic to blend in better as it would look like an admin doing their job. 
#### Get Imported Modules
```powershell
# lists modules currently imported into powershell session.
Get-Module

# Import a new module
Import-Module <module> 
Import-Module ActiveDirectory

# verify module was loaded
Get-Module
```

^65a4d8

#### Get Basic Domain Data
```powershell
# Displays basic AD information such as domain SID, domain functional level, child domains, etc.
Get-ADDomain
```

^d75542

#### Get Domain Users w/ ServicePrincipalName field populated
```powershell
# Uses cmdlet to dump all AD users then filter results by if their SerrvicePrincipalName is NOT null. 
Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName
```

^18aa48

#### Get Trust Relationships
```powershell
# Get any trust relationships i.e. any outside domains trusted by ours and vice versa. Displays the trusted domains and the trust relationship with them.
Get-ADTrust -Filter *
```

^fef682

#### Get AD Groups
```powershell
# Get the name of all AD Groups
Get-ADGroup -Filter * | select name

# Get detailed info on specific group by name
Get-AdGroup -Identity "<group name>"
Get-ADGroup -Identity "Backup Operators"

# Get group memebership of specific group
Get-ADGroupMember -Identity "<group name>"
Get-ADGroupMember -Identity "Backup Operators"
```

^bd8eb9

#### ACL Enum
```powershell
# Create a list of domain users, output to file for loop use later
Get-ADUser -Filter * | Select-Object -ExpandProperty SamAccountName > ad_users.txt

# use the userlist to enumerate ACLs
foreach($line in [System.IO.File]::ReadLines("C:\Users\htb-student\Desktop\ad_users.txt")) {get-acl  "AD:\$(Get-ADUser $line)" | Select-Object Path -ExpandProperty Access | Where-Object {$_.IdentityReference -match 'INLANEFREIGHT\\wley'}}
```

^a853cd

#### Enum if User saves password w/ reversible encryption
```powershell
Get-AdUser -Filter 'userAccountControl -band 128' -Properties userAccountControl
```

^dbd7a0

#### Establish WinRM Session
```powershell
# You need to create a secure string for your password, then feed it to a credentials object that will be fed to the cmdlet and used for authentication
$password = ConvertTo-SecureString "<passwd>" -AsPlainText -Force
$cred = new-oject System.Management.Automation.PSCredential ("<domain>\<usr>", $password)
Enter-PSSession -ComputerName <hostname> -Credential $cred

$password = ConvertTo-SecureString "Klmcargo2" -AsPlainText -Force
$cred = new-object System.Management.Automation.PSCredential ("INLANEFREIGHT\forend", $password)
Enter-PSSession -ComputerName ACADEMY-EA-MS01 -Credential $cred
```