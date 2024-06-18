-- -
Password hash cracking software. You can search for the most updated list of modes online [here](https://hashcat.net/wiki/doku.php?id=example_hashes) or you can search for the modes locally [[Hashcat modes|here]], but be aware that this may not be an updated list!
### Basic Usage
```bash
# NTLMv2 mode: 5600
hashcat -m <mode> <hash file> <wordlist> 
hashcat -m 5600 forend_ntlmv2 /usr/share/wordlists/rockyou.txt 
```
### Specific Targeted Cracking
##### kerberoasting
[[Dark Arts/Active Directory/Attacks/Kerberoasting|Get TGS Ticket]]
```bash
# crack NTLM password from TGS Ticket Hash
hashcat -m 13100 <hash file> <wordlist>
hashcat -m 13100 sqldev_tgs /usr/share/wordlists/rockyou.txt
``` 

^88073c
