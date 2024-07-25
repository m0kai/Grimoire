-- -
One of the maintained forks of deprecated PowerView. SharpView is in essence a port of  PowerView to a standalone binary rather than a PowerShell module and it is written in C#. 

#### Stealth considerations
Useful when a client has hardened against PowerShell usage or we need to avoid using PowerShell for any number of reasons. I doubt it's all that much stealthier outside of sidestepping hard filters on PowerShell but I could be wrong. 
#### Get help on function
```powershell
.\SharpView.exe Get-DomainUser -Help
```
#### Get Basic User info
```powershell
.\SharpView.exe Get-DomainUser -Identity <username> 
.\SharpView.exe Get-DomainUser -Identity forend
```

^db25de
