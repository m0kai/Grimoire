-- -
Interact with MSSQL using the Impacket-Toolkit.
#### Basic usage
```bash
# Connect to remote database
mssqlclient.py <domain>/<user>@<ip> -windows-auth
mssqlclient.py INLANEFREIGHT/DAMUNDSEN@172.16.5.150 -windows-auth

# Run system commands
enable_xp_cmdshell
xp_cmdshell <command>
xp_cmdshell whoami /priv
```

^7e7168
