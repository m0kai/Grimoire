-- -
Probably able to do more, but for now, just used to poison LLMNR/NBT-NS/MDNS. 
[wiki](https://github.com/Kevin-Robertson/Inveigh/wiki/Parameters)
#### Protocols
Inveigh can listen/poison the following protocols:
- IPv4
- IPv6
- LLMNR
- DNS
- mDNS
- NBNS
- DHCPv6 
- IMPv6
- HTTP
- HTTPS
- SMB
- LDAP
- WebDAV
- Proxy Auth
### InveighZero
Basically, the same as the original (below), but written entirely in `C#` so it can be compiled into a binary.
Hit the ESC key to enter/exit interactive console.
```powershell
# Run the binary
.\Inveigh.exe

# From interactive console
HELP # gives help menu

GET NTLMV2UNIQUE # Display captured hashes
GET NTLMV2USERNAMES # Display collected usernames
```

^675aa5

### Powershell Implementation (Depricated)
#### Basic Usage
```powershell
Import-Module .\Inveigh.ps1 # import module to start using it
(Get-Command Invoke-Inveigh).Parameters # get commands you can use i.e. "help"
```
#### LLMNR/NBT-NS/MDNS Poisoning
```powershell
# Prints output to stdout and to an output file
Invoke-Inveigh Y -NBNS Y -ConsoleOutput Y -FileOutput Y
```

^72b71f
