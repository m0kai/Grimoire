-- -
Find out the mail server(s) used by a domain.
### Host
```bash
# get mail servers for the specified domain
host -t MX <domain>
host -t MX inlanefreight.htb

# get A record of mail server
host -t A <mail server> 
host -t A mail1.inlanefreight.htb
```
### Dig
```bash
dig mx <domain(s)> | grep "MX" | grep -v ";"
dig mx inlanefreight.com | grep "MX" | grep -v ";"
```