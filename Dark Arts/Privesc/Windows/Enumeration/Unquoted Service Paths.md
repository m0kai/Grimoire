-- -
As it sounds, you know what this is. The service has a path that includes a space (and isn't inside quotation marks!) in it so you just make sure to have control of (or make your own) directory of the first word before the space, then put your malware in that directory so that when the service goes to run, it picks up your malware thinking it found the right program and stops looking for the actual program.

For example, if the path is `C:\Program Files\service.exe`, you put your malware in `C:\Program.exe`, and that gets picked up before the first path. 

#### winpeas.exe
You can also get this information using winpeas.exe for enumeration. 
#### Using PowerUp.ps1
[[Windows|File Transfer]] `PowerUp.ps1` to target host
```powershell
# if in cmd
powershell -ep bypass

# load PowerUp
. .\PowerUp.ps1

Invoke-AllChecks

# will output:
# [*] Checking unquoted service paths...
# Then spits out any services with unquoted service paths.
# It will output the vulnerable path and will output the function/command to use w/ PowerUp to abuse it. 

# for this example, lets say the unquoted path is:
# C:\Program Files\Unquoted Path Service\Common Files\unquotedpathservice.exe

# to further enumerate the service:
sc query <service> 
sc query unquotedsvc
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
Use the command is suggests, or [[Dark Arts/Privesc/Windows/Exploits/Unquoted Service Paths|Exploit]] with my notes