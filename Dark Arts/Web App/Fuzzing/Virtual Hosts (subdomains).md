-- -
Multiple virtual hosts per single IP. Is (generally) controlled via the `Host` HTTP header. So you fuzz the header using the same IP address and see what you get. Generally what you will use for CTFs and the like. 
### ffuf
```bash
ffuf -u http://<ip> -w <wordlist path> -H 'Host:FUZZ.<hostname>'
ffuf -u http://10.10.10.10 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -H 'Host: FUZZ.academy.htb'
```
### gobuster
```bash
# helpful flags
# -t: thread count
# -k: ignore SSL/TLS
# -o: output file
gobuster vhost http://<ip> -w <wordlist path> --append-domain
gobuster vhost -u http://inlanefreight.htb:81 -w /usr/share/seclists/Discovery/DNS/subdomains-top1million-110000.txt --append-domain 
```