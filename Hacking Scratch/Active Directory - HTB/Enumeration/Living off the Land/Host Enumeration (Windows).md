-- -
For situations when you are on a Windows host and **do not** have the ability to load tools in thus are required to only use builtin tools for enumeration.
#### Initial Recon
```powershell
# Prints PC Hostname
hostname

# OS version/revision level
[System.Environment]::OSVersion.Version

# Applied Patches and hotfixes
wmic qfe Caption,Description,HotFixID,INstalledOn 

# Network adapter state and config
ipconfig /all 
# Env variable for current session (cmd)
set

# Domain name computer is connected to (cmd)
echo %USERDOMAIN%

# DC used for authentication (cmd)
echo %logonserver%

# everything the above commands display (less noise)
systeminfo
```
#### Useful PowerShell cmdlets
![[Hacking Scratch/Tools/Windows Builtin/PowerShell#^70bbe9|PowerShell]]
![[Hacking Scratch/Tools/Windows Builtin/PowerShell#^5e02c8|PowerShell]]
#### Downgrade PowerShell
This would be done in order to disable logging on our session and afford us further stealth as the SOC should be more blind without logs in the `Event Log`. To verify, go to the `PowerShell Operation Log` located at `Applications and Service Logs`->`Microsoft`->`Windows`->`Powershell`->`Operational`. You can also check at location: `Applications and Service logs`->`Windows PowerShell`. 
![[Hacking Scratch/Tools/Windows Builtin/PowerShell#^5ccc63|PowerShell]]
*Note that the downgrade command (and anything before it) will still be logged, so a vigilant defender may notice the downgrade and open an investigation from there.*
#### Enum Defenses
![[Hacking Scratch/Tools/Windows Builtin/PowerShell#^092be7|PowerShell]]
#### Enum Logged on Users
If you take actions on a host someone else is logged into, then you may alert them of your activities and get it reported so you want to know if anyone else is on the host you are interacting with.
![[Hacking Scratch/Tools/Windows Builtin/PowerShell#^3fad5e|PowerShell]]
#### Windows Management Instrumentation Enum
Used by administrators for automation of Windows environments. 
![[Windows Management Instrumentation (WMI)#^a7f69f]]