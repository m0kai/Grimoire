-- -
You are checking if there are any services that have FILE_ALL_ACCESS permissions set and have an attached executable, if we can manipulate/replace the executable then run the service, we should get an elevated shell/add user to administrators group. 
#### Check services
May need to [[Windows|File Transfer]] it to target, but it should be a sysinternals program, so may already be on the file system. 
On Windows target box:
```powershell
# looking for:
# RW Everyone:
# FILE_ALL_ACCESS
# for filepermissionservice.exe
accesschk64.exe -wvu "C:\Program Files\File Permissions Service"
```
#### Using PowerUp.ps1
You will need to [[Windows|file transfer]] it to target.
```powershell
# if on cmd, open powershell
powershell -ep bypass

# Load PowerUp.ps1 
. .\PowerUp.ps1

# outputs a lot of stuff, but in the output:
# Checking service executable and argument permissions...
# then it dumps out services with executables attached
Invoke-AllChecks
```