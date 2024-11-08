-- -
This is a (somewhat) niche problem that **may** pop up, but is (at time of writing) unlikely. The main point of contention is if the box you land on does not have `unconstrained delegation` enforced on it. If it **does** have `unconstrained delegation` enforced, then you won't run into this specific problem. 
### Problem
You get a user's password and are able to get a shell on it via [[Hacking Scratch/Tools/Active Directory/Windows/Evil-WinRM]] or something like that. The situation can arise where you do network authentication with the DC to get access to this shell, but due to using network authentication and a lack of `unconstrained delegation`, the password is not put into memory/cached with your session. So when you try to do anything else in the domain, it fails. You basically get a kerberos ticket to access the one system, but the ticket itself is only valid for the shell on that system. When you try to query the DC for information, for example, you would need to re-authenticate with the DC so you get a TGS for that query, but since the credentials were not cached with your session, the DC cannot authenticate you to further services and you are explicitly denied. 
### Workarounds
[Resource](https://posts.slayerlabs.com/double-hop/)
Since the password isn't cached, but you do know it, then you just need to bundle the password with your new request/query explicitly. 
#### Explicitly include credentials with each command
This situation is basically if you are connected to the host via winrm and are trying to load in PowerView but get the following error:
```powershell
*Evil-WinRM* PS C:\Users\backupadm\Documents> get-domainuser -spn
Exception calling "FindAll" with "0" argument(s): "An operations error occurred.
"
At C:\Users\backupadm\Documents\PowerView.ps1:5253 char:20
+             else { $Results = $UserSearcher.FindAll() }
+                    ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : NotSpecified: (:) [], MethodInvocationException
    + FullyQualifiedErrorId : DirectoryServicesCOMException
```
You can check if your credentials are cached in the session:
```bash
klist
```
If you only see your ticket, then that is why you are getting the above error, so just create a credentials object and pass it into each powerview command:
```powershell
# Create credentials object
$SecPassword = ConvertTo-SecureString '!qazXSW@' -AsPlainText -Force
$Cred = New-Object System.Management.Automation.PSCredential('INLANEFREIGHT\backupadm', $SecPassword)

# pass to PowerView
get-domainuser -spn -credential $Cred | select samaccountname
```
#### Add credentials to PSsession config
1. Register your credentials with PSSession Configuration
2. Restart WinRM service
3. Reconnect to host
```powershell
# Step 1:
# Setup config, note the name you give it, you will provide this later
Register-PSSessionConfiguration -Name backupadmsess -RunAsCredential inlanefreight\backupadm

# Step 2: 
# Restart service, emember you will be kicked off
Restart-Service WinRM

# Step 3:
# connect back, notice we connect and specify which configuration we want, which should match what config you set it to above
Enter-PSSession -ComputerName DEV01 -Credential INLANEFREIGHT\backupadm -ConfigurationName  backupadmsess
```