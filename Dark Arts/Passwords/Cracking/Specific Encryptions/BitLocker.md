-- -
Doing a vanilla `bitlocker2john` will produce 4 different hashes that can all be cracked. If using hashcat, you will need to separate the hashes out bc they require different modes. 
```bash
# extract hashes
bitlocker2john -i <file>.vhd > backup.hashes

# pull out the bitlocker password, i.e. the first hash
grep "bitlocker\$0" backup.hashes > bakup.hash
hashcat -m 22100 backup.hash rockyou.txt -o backup.cracked
cat backup.cracked
```
### opening bitlocker vDrive
Easiest way to do this is to get it onto a windows machine and mount it. You just need to double click the file, it should be recognized as a virtual drive by windows after you transfer it. 