-- -
#### LDAP Anonymous bind user enum
```bash
# uses LDAP anonymous bind to try to enumerate users in AD
# -u: username, blank for anonymous 
# -U: enumerate usernames
./windapsearch.py --dc-ip <dc ip> -u "" -U
```

^2767f4

#### Enum Domain Admins (auth)
```bash
python3 windapsearch.py --dc-ip <dc ip> -u <user>@<domain> -p <passwd> --da
```

^c4f0a5

#### Enum privileged users (auth)
```bash
# recursively search for privileged users, recursively check group membership
python3 windapsearch.py --dc-ip <dc ip> -u <user>@<domain> -p <passwd> -PU
```

^bfae1e
