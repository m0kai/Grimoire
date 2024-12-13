-- -
Technically this is for the RPC service, but RPC only shows up in conjunction w/ SMB. You can reference this [cheatsheet](https://www.willhackforsushi.com/sec504/SMB-Access-from-Linux.pdf) or the [man pages](https://www.samba.org/samba/docs/current/man-html/rpcclient.1.html) for detailed information on the tool.
### Null Session Basic Usage
```bash
# connect to RPC service on target
rpcclient -U'%' <ip> 

# enumerate users
enumdomusers
```