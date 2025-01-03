-- -
### Linux
-- -
##### netexec
```bash
netexec smb <ip> -u <user> -p <passwd> --pass-pol
```
### Windows
-- -
##### net (cmd)
```powershell
net accounts
```
##### PowerView
```powershell
import-module .\PowerView.ps1
Get-DomainPolicy
```