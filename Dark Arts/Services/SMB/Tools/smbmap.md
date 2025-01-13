-- -
### Basic Usage w/ Null Session
```bash
# scan avaialable shares 
smbmap -H <ip>

# scan share for files/directories
smbmap -H <ip> -r <share>
smbmap -H <ip> -R <share>

# download file
smbmap -H <ip> --download "<share>\<file>"

# upload file
smbmap -H <ip> --upload <file> "<share>\<file>"
```