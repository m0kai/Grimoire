-- -
Password hash cracking software. You can search for the most updated list of modes online [here](https://hashcat.net/wiki/doku.php?id=example_hashes) or you can search for the modes locally [[Hashcat modes|here]], but be aware that this may not be an updated list!
### Basic Usage
```bash
# NTLMv2 mode: 5600
hashcat -m <mode> <hash file> <wordlist> 
hashcat -m 5600 forend_ntlmv2 /usr/share/wordlists/rockyou.txt 

# Optimized i.e. faster on metal
hashcat -m 5600 hash /usr/share/wordlist/rockyou.txt -O

# using a good ruleset to permutate you guesses
# One Rule to rule them all
hashcat -m 5600 hash /usr/share/wordlist/rockyou.txt -r OneRule
```
### Specific Targeted Cracking
##### kerberoasting
[[Hacking Scratch/Active Directory - HTB/Attacks/Kerberoasting|Get TGS Ticket]]
```bash
# crack NTLM password from TGS Ticket Hash
hashcat -m 13100 <hash file> <wordlist>
hashcat -m 13100 sqldev_tgs /usr/share/wordlists/rockyou.txt
``` 

^88073c

##### ASREPRoasting
[[ASREPRoasting]]
```bash
hashcat -m 18200 hash /usr/share/wordlists/rockyou.txt
```

^364f87
