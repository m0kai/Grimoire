-- -
### Basic Usage w/ Null Session
```bash
# scan avaialable shares 
smbmap -H <ip>

# scan available shares w/ creds
smbmap -u [user] -p [passwd] -d [domain] -H [ip]

# Recursively scan share for files/directories
smbmap -H <ip> -r <share>
smbmap -H <ip> -R <share>

# download file
smbmap -H <ip> --download "<share>\<file>"

# upload file
smbmap -H <ip> --upload <file> "<share>\<file>"
```

^ad4ec0
