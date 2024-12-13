-- -
Search the filesystem for files w/ credentials.
### Key terms
Key search terms to try to narrow down your searches:
```bash
Passwords
Passphrases
Keys
Username
User account
Creds
Users
Passkeys
Passphrases
configuration
dbcredential
dbpassword
pwd
Login
Credentials
```
## Search bar
If you have GUI access, hit the windows button or click the search bar at the bottom right of the search then search the above terms and see if anything interesting comes up. 
### Lazagne
Third-party tool to search the file system for us. [[Dark Arts I/File Transfer/~Home|File Transfer]] the binary over to the target machine first. 
```powershell
# cmd works as well
# use -vv for verbosity
start lazagne.exe all
```
### findstr
searches for a provided string in files on the file system. This one should be builtin to cmd and powershell.
```powershell
findstr /SIM /C:"password" *.txt *.ini *.cfg *.config *.xml *.git *.ps1 *.yml

# look for sensitive info in files
findstr /s /i <string> <location>\*.*
findstr /s /i cred C:\*.*

# in powershell, you can accomplish the same thing with the Select-String cmdlet
Get-ChildItem -Recurse -Path N:\ | Select-String "cred" -List
```
Further [examples](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/findstr#examples) of `findstr`
### Dir
Search for interesting file names
```powershell
dir <location>\*<str>* /s /b 
dir n:\*cred* /s /b
n:\*secret* /s /b 

# in powershell you can do the same thing with the Get-ChildItem cmdlet
Get-ChildItem -Recurse -Path N:\ -Include *cred* -File
```
### Where to look
A few places to consider
- Passwords in Group Policy in the SYSVOL share
- Passwords in scripts in the SYSVOL share
- Password in scripts on IT shares
- Passwords in web.config files on dev machines and IT shares
- unattend.xml
- Passwords in the AD user or computer description fields
- KeePass databases --> pull hash, crack and get loads of access.
- Found on user systems and shares
- Files such as pass.txt, passwords.docx, passwords.xlsx found on user systems, shares, [Sharepoint](https://www.microsoft.com/en-us/microsoft-365/sharepoint/collaboration)