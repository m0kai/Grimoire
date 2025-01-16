-- -
A .NET (C#) port of [[Dark Arts/Tools/Active Directory/PowerView|PowerView]]. Compiled to an executable rather than distributed as a PowerShell module.

SharpView is helpful for situations when PowerShell has been hardened and/or restricted and we don't/can't use PowerShell effectively. 
### Get Argument List for a specific method
```powershell
SharpView.exe [method] -Help
.\SharpView.exe Get-DomainUser -Help
```
### Basic Usage
```powershell
Sharpview.exe Get-DomainUser -Identity [user]
.\SharpView.exe Get-DomainUser -Identity forend
```