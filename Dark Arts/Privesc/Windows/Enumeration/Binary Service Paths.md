-- -
Hijacking the path of a binary.
#### Using PowerUp.ps1
[[Dark Arts/File Transfer/Windows|File Transfer]] `PowerUp.ps1` to target host
```powershell
# if in cmd
powershell -ep bypass

# load PowerUp
. .\PowerUp.ps1

Invoke-AllChecks

# will output:
# [*] Checking service permissions...
# and after will display vulnerable services, it will also tell you which PowerUp function to use to abuse the service. Another big item to look at is:
# CanRestart: True
# this means we can restart the service ourselves after compromise to get it to run whatever we want. 
```
If the above method of running PowerUp does not work because you can't load up powershell, you can one line it:
```bash
# on your attack box edit the PowerUp.ps1 file and include the command it should run after loading:
Invoke-AllChecks
```
Then, [[Dark Arts/File Transfer/Windows|File Transfer]] the script over to the target box. 
Then on the shell just run:
```powershell
powershell -ep bypass .\PowerUp.ps1
```
#### Using Accesschk64.exe
[[Dark Arts/File Transfer/Windows|File Transfer]] `accesschk64.exe` to target host
```powershell
# u: suppress errors
# v: verbose
# w: only show object w/ write access
# c: Display Service Name
# check for objects that meet above criteria that everyone on the system has access to. 
accesschk64.exe -uwcv Everyone *

# this will hopefully output a service we can abuse, in this example the service is:
# daclsvc
# after you find a vulnerable service, verify further by using accesschk against that service specifically, same as above but to the service
accesschk64.exe -uwcv daclsvc

# under here you want to see:
# RW Everyone
# SERVICE_CHANGE_CONFIG
```
From here [[Dark Arts/Privesc/Windows/Exploits/Binary Service Paths|Exploit]]
