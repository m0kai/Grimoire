-- -
My preferred cracker. 
### Cracking unshadowed hashes
```bash
# 1800 should be for SHA-512 ($6$) hashes
hashcat -m 1800 -a 0 unshadowed.hashes rockyou.txt -o unshadowed.cracked

# 500 for md5 hashes
hashcat -m 500 -a 0 md5-hashes rockyou.txt
```