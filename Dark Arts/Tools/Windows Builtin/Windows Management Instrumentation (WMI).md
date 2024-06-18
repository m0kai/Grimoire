-- -
A scripting engine used for automation of administrative tasks in a Windows environment. 

[Cheatsheet](https://gist.github.com/xorrior/67ee741af08cb1fc86511047550cdaf4)
#### Quick Checks
```powershell
# List Patch level and description of Hotfixes applied to host
wmic qfe get Caption,Description,HotFixID,InstalledOn

# Basic host info
wmic computersystem get Name,Domain,Manufacturer,Model,Username,Roles /format:List

# List all processes on host
wmic process list /format:list

# Display Domain/DC Information
wmic ntdomain list /format:list

# Display local/domain account info for accounts that have logged into the host.
wmic useraccount list /format:list

# Local Group Info
wmic group list /format:list

# Dumps system account info 
wmic sysaccount list /format:list 
```

^a7f69f
