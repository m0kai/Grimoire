-- -
Executable for ingesting AD data that can be imported into Bloodhound for visualization. It is an `.exe` file, so it's expected to be transferred to compromised windows host and run from there. 
#### Basic Usage
```powershell
# -c: collection method, set to all
# --zipfilename: the name of the output zip file you will uplaod to Bloodhound
.\SharpHound.exe -c <collection method> --zipfilename <output filename> 
.\SharpHound.exe -c All --zipfilename ILFREIGHT
```