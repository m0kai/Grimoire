-- -
A config that is set in the registry that allows MSI programs to always be installed with elevated privileges. So, if you find this you can create a malicious msi, file transfer it over, run it and get an elevated shell. 

#### Search registry
Search the registry for AlwaysInstallElevated set to 1
```powershell
# look for AlwaysInstallElevated set to 1
reg query HKLM\Software\Policies\Microsoft\Windows\Installer
reg query HKCU\Softwar\Policies\Microsoft\Windows\Installer
```
From here, [[Dark Arts/Privesc/Windows/Exploits/AlwaysInstallElevated|Exploit]]
#### Using PowerUp.ps1
You will need to [[Windows|file transfer]] it to target.
```powershell
# if on cmd, open powershell
powershell -ep bypass

# Load PowerUp.ps1 
. .\PowerUp.ps1

# outputs a lot of stuff, but in the output, you can find the AlwaysInstallElevated setting
Invoke-AllChecks

# will output something like:
# [*] Checking for AlwaysInstallElevated registry key...
# AbuseeFunction : Write-UserAddMSI
```
If the above method of running PowerUp does not work because you can't load up powershell, you can one line it:
```bash
# on your attack box edit the PowerUp.ps1 file and include the command it should run after loading:
Invoke-AllChecks
```
Then, [[Windows|File Transfer]] the script over to the target box. 
Then on the shell just run:
```powershell
powershell -ep bypass .\PowerUp.ps1
```
From here, [[Dark Arts/Privesc/Windows/Exploits/AlwaysInstallElevated|Exploit]]