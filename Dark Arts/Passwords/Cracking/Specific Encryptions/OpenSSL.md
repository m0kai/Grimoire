-- -
Note that the following will produce a ton of errors, but if successful, it will produce a new file you can uncompress. 
```bash
for i in $(cat rockyou.txt);do openssl enc -aes-256-cbc -d -in file.gzip -k $i 2>/dev/null| tar xz;done
```