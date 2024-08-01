-- -
Take over a registry service for NT AUTHORITY.
#### Check ACL registry
```powershell
# Output shoudl suggest that user belongs to NT AUTHORITY\INTERACTIVE and has FullControl permissions over the registry key

# should look like:
# Access : Everyone Allow ReadKey
# NT AUTHORITY\INTERACTIVE Allow FullControl
Get-Acl -Path hklm:\System\CurrentControlSet\services\regsvc | fl
```
From here [[Dark Arts/Privesc/Windows/Exploits/Regsvc ACL|exploit]]