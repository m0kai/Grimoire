-- -
Check if various security controls are on a Windows System.
### General
```powershell
# Windows Defender
Get-MpComputerStatus

# Powershell is regularly blocked on normal workstations, but you may find a useable powershell executable they forgot to block:
# %SystemRoot%\SysWOW64\WindowsPowerShell\v1.0\powershell.exe
# %SystemRoot%\system32\WindowsPowerShell\v1.0\powershell.exe

# AppLocker Policy, i.e. AppLocker is a whitelist of appications that can or cannot be run on the system/by the user. 
Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections

# PowerShell can also be allowed, but restricted. Constrained Language Mode allows PowerShell to be run, but in a limited fashion. You can see if Constrained Language Mode is on the current session by looking at the following environmental variable 
$ExecutionContext.SessionState.LanguageMode
```
### LAPS
Find groups with LAPS enabled
```powershell
Find-LAPSDelegatedGroups
```
Find groups with "All Extended Rights" applied to their users. Allows these users to read LAPS passwords and have the same control over any system with LAPS applied
```powershell
Find-AdmPwdExtendedRights
```
Search for computer w/ LAPS enabled
```powershell
Get-LAPSComputers
```