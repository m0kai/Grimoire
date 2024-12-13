-- -
### Cracking file passphrases
For when files (id_rsa) are encrypted and you want to crack the password to open/use the file. Note that you can use the hash in the output with hashcat as well, just not the full output. 
```bash
# locate correct script
locate *2john*

# note that the following works for most office documents (word, excel, powerpoint, etc)
office2john <file> > hash

# process/commands should look the same for each script
ssh2john.py <encrypted file> > hash

# then crack like normal
john --wordlist=rockyou.txt hash

# show cracked password
john hash --show
```