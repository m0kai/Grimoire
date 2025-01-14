-- -
Technically this is for the RPC service, but RPC only shows up in conjunction w/ SMB. You can reference this [cheatsheet](https://www.willhackforsushi.com/sec504/SMB-Access-from-Linux.pdf) or the [man pages](https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html) for detailed information on the tool.
### Null Session Basic Usage
```bash
# connect to RPC service on target
rpcclient -U'%' <ip> 

# connect to RPC via NULL session
rpcclient -U "" -N [ip]

# enumerate users
enumdomusers
```
### Enum User Info 
```bash
# after you are connected, you can enumerate user information using the RID value for a user. In this case we are using the RID for the local admin account, which will always be this value no matter the domain.
# Note that doing the enumdomusers will spit out all the user's RIDs for the domain. 
query user 0x1f4
```

^2ccb10
