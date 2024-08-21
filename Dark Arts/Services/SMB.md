-- -
### Null Session Listing
```bash
# list out available shares and log in with a null session
smbclient -N -L //10.10.10.10
```
### Connect to Share
```bash
# default domain: WORKGROUP
# default user: your computer username
# will ask for password
smbclient //10.10.10.10/notes
```
### Download Files
```bash
get <file> 
```