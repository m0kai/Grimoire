-- -
### Status updates
Set nmap to automatically show you status updates as it goes
```bash
# can be seconds: 5s
# or minutes: 10m
nmap 10.10.10.10 -p- --stats-every=5s
```
### Verbosity
```bash
# -v or -vv depending on level of verbosity you want
nmap 10.10.10.10 -v
nmap 10.10.10.10 -vv
```
### Debugging 
Get more details about what nmap is doing what its doing
```bash
# verbose, shows packet trace i.e. everything happening
nmap 10.129.2.18 --packet-trace

# --reason: nmap explains why a port is marked as it is
nmap 10.129.2.18 --reason
```