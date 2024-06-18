-- -
Query Active Directory objects. You can basically use the same queries as you would for [[Cypher Queries|BloodHound]] or [[PowerView (depricated)|PowerView]]. 
#### Requirements
More likely to be on systems utilized by Domain sysadmins. Exist on any host with the `Active Directory Domain Services Role` installed. The DLL for dsquery should exist on all modern Windows systems by default and can be found at `C:\Windows\System32\dsquery.dll`.
### Basic Usage
```powershell
# may require a system context.
# Can run on PowerShell or CMD

# User search
dsquery user

# Computer Search
dsquery computer

# Wildcard search for all objects in an OU
dsquery * "CN=Users,DC=INLANEFREIGHT,DC=LOCAL"

# Can be combined with LDAP serach filters as the following:

# Example LDAP filter:
# userAccountControl:1.2.840.113556.1.4.803:=8192
# ^ uses bitwise ops to filter, like regex but with bitwise numbers
# way too complicated to dive deep into right now, but wanted to mention it here so if I need to dive into this, I can. 

# Look for users with the following attributes set:
# PASSWD_NOTREQD
# userAccountControl
dsquery * -filter "(&(objectCategory=person)(objectClass=user)(userAccountControl:1.2.840.113556.1.4.803:=32))" -attr distinguishedName userAccountControl

# Search for Domain Controllers, limit results to 5
dsquery * -filter "(userAccountControl:1.2.840.113556.1.4.803:=8192)" -limit 5 -attr sAMAccountName
```

^d1a517
