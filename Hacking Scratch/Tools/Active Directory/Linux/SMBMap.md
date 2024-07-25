-- -
Used to enumerate SMB shares. You can list out available shares and permissions to those shares as well as download and upload files, and execute remote commands.
#### List available shares and share permissions (domain auth)
```bash
smbmap -u <user> -p <passwd> -d <domain> -H <target ip>
```

^64bb50

#### Directory list of a share (domain auth)
```bash
smbmap -u <user> -p <passwd> -d <domain> -H <target ip> -R '<share name>' --dir-only
```

^cc7a8d
