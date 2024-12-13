-- -
#### NT/NTLM hashes
```bash
# Cracking NT Hash
# second part of SAM dump hash, after semicolon
hashcat -m 1000 hash <wordlist> 

# Cracking NTLM hashes
# full thing w/ username
hashcat -m 5600 hash <wordlist>
```

^24472d

#### TGS Ticket Hashes
```bash
hashcat -m 13100 hash <wordlist>
```

^678be7
