-- -
#GPO
#### Get Names of GPOs in use
**PowerView**
![[PowerView (depricated)#^ad0a90]]
**PowerShell builtin cmdlet**
![[Dark Arts/Tools/Active Directory/Windows/PowerShell#^a53af2|PowerShell]]
#### Enumerate Domain User GPO Rights
enumerate Domain User's rights over one or more GPOs, but may also be that they have NO rights over any GPOs.
![[PowerView (depricated)#^a2d830]]
#### Convert GPO GUID to Name
Doing the above *Enumerating Domain User GPO rights* should yield one or more GPO GUIDs, which can be found in the `ObjectDN` field. To convert this GUID into an easily understandable name, do the following:
![[Dark Arts/Tools/Active Directory/Windows/PowerShell#^997a51|PowerShell]]
Then lookup that name in bloodhound to see what you can do with it. 