-- -
#### LDAP Anonymous bind user enum
```bash
# uses LDAP anonymous bind to try to enumerate users in AD
# -u: username, blank for anonymous 
# -U: enumerate usernames
./windapsearch.py --dc-ip <dc ip> -u "" -U
```

^2767f4
