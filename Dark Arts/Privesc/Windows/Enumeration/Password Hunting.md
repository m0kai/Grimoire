-- -
##### General
```powershell
# only searches pwd
# only searches in .txt files
findstr /si password *.txt

# you can add ass many extensions as you want
findstr /si password *.txt *.ini *.conf
```
##### Registry
Check registry entries for default passwords or just cleartext passwords. This will dump a lot of registry entries so it will be a lot to sift through, but it can be a quick win w/ a password.
```bash
# general search for passwords in registry
reg query HKLM /f password /t REG_SZ /s

# windows autologin
reg query "HKLM\SOFTWARE\Microsoft\Windows NT\Currentversion\Winlogon"
```
### Resources
- [PayloadAllTheThings](https://swisskyrepo.github.io/InternalAllTheThings/redteam/escalation/windows-privilege-escalation/#eop-looting-for-passwords)is you friend