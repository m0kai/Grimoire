-- -
Often, automation scripts for system admins are in the `SYSVOL` share on a dc so they are easily accessible across the domain. It is a good idea to dig through this share to see if you can find any hard coded credentials. It is likel y what you find are old accounts and old passwords that may or may not still be in use, but it gives you some credentials to work with for password spraying or seeing if you can use them to log into any of the systems on the network.
### Example
**Check contents of SYSVOL script directory**
```powershell
ls \\academy-ea-dc01\SYSVOL\INLANEFREIGHT.LOCAL\scripts
```

which outputs:
```
Directory: \\academy-ea-dc01\SYSVOL\INLANEFREIGHT.LOCAL\scripts


Mode                LastWriteTime         Length Name                            ----                -------------         ------ ----                            -a----       11/18/2021  10:44 AM            174 daily-runs.zip                  -a----        2/28/2022   9:11 PM            203 disable-nbtns.ps1               -a----         3/7/2022   9:41 AM         144138 Logon Banner.htm                -a----         3/8/2022   2:56 PM            979 reset_local_admin_pass.vbs 
```

The `reset_local_admin_pass.vbs` looks interesting:
```vb
cat \\academy-ea-dc01\SYSVOL\INLANEFREIGHT.LOCAL\scripts\reset_local_admin_pass.vbs

On Error Resume Next
strComputer = "."
 
Set oShell = CreateObject("WScript.Shell") 
sUser = "Administrator"
sPwd = "!ILFREIGHT_L0cALADmin!"
 
Set Arg = WScript.Arguments
If  Arg.Count > 0 Then
sPwd = Arg(0) 'Pass the password as parameter to the script
End if
 
'Get the administrator name
Set objWMIService = GetObject("winmgmts:\\" & strComputer & "\root\cimv2")

<SNIP>
```

Then feed the sUser and sPwd values to crackmapexec
![[crackmapexec#^d499fd]]