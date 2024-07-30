-- -
##### General
```powershell
# Includes:
# Hostname
# OS Version
# Architecture
# etc
systeminfo

# more targetted
systeminfo | findstr /D /C:"OS Name" /C:"OS Version" /C:"System Type"

# get only hostname
hostname
```
##### Patch Information
```powershell
# get patch info, hot fixes applied, patches applied to system and such
# key item is the HotFixID
wmic qfe

# more targetted
wmic qfe get Caption,Description,HotFixID,InstalledOn
```
#### Disk Drive information
```powershell
# get info on drives available
wmic logicaldisk

# more targetted and cleaner
wmic logicaldisk get caption,description,providername

# get only the drive name
wmic logicaldisk get caption

# cleaner drive info
list drives
```