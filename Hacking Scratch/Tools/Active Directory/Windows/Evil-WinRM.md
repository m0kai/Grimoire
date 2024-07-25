-- -
Used to establish a shell on a windows system via WinRM. Will likely need credentials
#### Install
```bash
# it's a ruby gem so you can use that to install
gen install evil-winrm
```
#### Connect to Shell
```bash
evil-winrm -i <ip> -u <user>
evil-winrm -i 10.129.201.234 -u forend
```

^0229bc
