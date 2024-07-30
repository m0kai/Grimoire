-- -
```powershell
# get info on Windows Defender/Windows Security
sc query windefend

# dumps out all the services, which can be a lot but it will allow you to see any defenses running on the system, AVs other than windows defender.
sc queryex type= service

# firewall info
# more "modern"
netsh advfirewall firewall dump

# firewall info
# more "old"
netsh firewall show state

# show firewall config
# look for ports that may be open
netsh firewall show config
```