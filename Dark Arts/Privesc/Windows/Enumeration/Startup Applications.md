-- -
#### Enum startup apps/permissions
```powershell
# Looking for:
# BUILTIN\Users:<F>
# The <F> means full access
icacls.exe "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup"
```
From here [[Dark Arts/Privesc/Windows/Exploits/Startup Applications|exploit]]
