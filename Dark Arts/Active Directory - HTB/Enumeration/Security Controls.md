-- -
After getting an initial foothold, it is useful to get to know the environment. Specifically, see what protections are in place in AD and on the host you are accessing. This can determine the tools, tactics, and techniques you can/will use. 
#### Microsoft Defender
Enumerating Windows Defender on the host. It being the gigachad it is, this will determine if you need to go evasive or use built-in tools for enumeration rather than things like PowerView. 
```powershell
# use powershell to query Microsoft Defender
Get-MpComputerStatus

# you will be looking for the field:
# RealTimeProtectionEnabled
# if it's set to True, then Microsoft Defender is enabled on the system. 
```
#### AppLocker
Microsoft's application whitelisting solution. It will be setup to only allow certain software to exist or be run on the system. It provides system administrators granular control over which of the following are allowed to exist and run on the system:
- Executables
- Windows installer files
- DLLs
- packaged apps
- Packaged app installers
It is common for `cmd.exe` and `PowerShell.exe` to be blocked. It is also common for system administrators to forget about other PowerShell Executable locations such as:
- `%SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe`
- `PowerShell_ISE.exe`
So depending on which executable is blocked, we can sidestep AppLocker restrictions by using PoweShell from a different location. 
```powershell
# get AppLocker settings
Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections
```
User the above command to see which executables are blocked and see if you can use PowerShell from a location not listed. 
#### PowerShell Constrained Language Mode
PowerShell can be set to Constrained Language Mode which locks down many of the features needed to user PowerShell effectively, such as blocking:
- COM objects
- Unapproved .NET types
- XAML-based workflows
- PowerShell classes
- etc
```powershell
# will output:
# Contrained Language
# Full Language Mode
$ExecutionContext.SessionState.LanguageMode
```
#### LAPS
Microsoft `Local Administrator Password Solution` is used to randomize and rotate local administrator passwords on Windows hosts to prevent lateral movement. 
Check for LAPS delegated groups, which will likely be more restricted:
```powershell
Find-LAPSDelegatedGroups
```
Look for groups that have `All Extended Rights` and can read passwords and such:
```powershell
Find-AdmPwdExtendedRights
```
Search for computers with LAPS enabled:
```powershell
Get-LAPSComputers
```