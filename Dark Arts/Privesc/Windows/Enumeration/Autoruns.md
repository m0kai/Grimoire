-- -
Programs automatically. You are looking for automatically run programs with elevated privs we can exploit.
#### Look at Autorun programs
May need to [[Windows|File Transfer]] it to target, but it should be a sysinternals program, so may already be on the file system. 
```powershell
# dump all autoruns on the system
# In this example, it is located at:
# C:\Users\Desktop\Tools\Autoruns\
Autoruns64.exe

# you are looking for something that looks custom or weird, once you have proceed to next step to check its permissionas.
```
#### Check autorun permissions
Another sysinternals tool, may be on the system already or you may need to [[Windows|file transfer]] it over to the target. 
```powershell
# in this example, it is located at:
# C:\Users\User\Desktop\Tools\Accesschk\
accesschk64.exe -wvu "C:\Program Files\Autorun Program"

# looking for a program that has:
# RW Everyone
# FILE_ALL_ACCESS
# for the weird program identified above
```
#### Using PowerUp.ps1
You will need to [[Windows|file transfer]] it to target.
```powershell
# if on cmd, open powershell
powershell -ep bypass

# Load PowerUp.ps1 
. .\PowerUp.ps1

# outputs a lot of stuff, but in the output, you can find the autorun programs and see the permissions those programs have.
Invoke-AllChecks
```
After you identify a potentional vulnerable autorun program, proceed to [[Dark Arts/Privesc/Windows/Exploits/Autoruns|Exploit]]
