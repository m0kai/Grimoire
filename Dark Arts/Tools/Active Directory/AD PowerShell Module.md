-- -
The Active Directory PowerShell Module is a collection of PowerShell cmdlets for administering an Active Directory environment. In other words, builtin PowerShell module for AD.
### Check imported PowerShell Modules
Check if Active Directory module is imported to current session
```powershell
Get-Module
```
### Import Active Directory Module
If not automatically present, import the module
```powershell
# import module
Import-Module ActiveDirectory

# check it was imported successfully
Get-Module
```
### General Enum
```powershell
# get general AD info such as:
# Domain SID
# Domain Functional Level
# Child Domains
Get-ADDomain

# Enum Users
Get-ADUser

# Enum groups, get the names of groups in the domain
Get-ADGroup -Filter * | select name

# get detailed group info
Get-ADGroup -Identity "[group name]"

# Get group membership info
Get-ADGroupMember -Identity "[group name]"
```
### Get Kerberoasting targets
```powershell
# Enum users with a Service Principal Name, meaning these will be accounts that may be suceptible to Kerberoasting
Get-ADUser -Filter {ServicePrincipalName -ne "$null"} -Properties ServicePrincipalName
```

^67a0eb
### Check Domain Trust Relationships
```powershell
Get-ADTrust -Filter *
```