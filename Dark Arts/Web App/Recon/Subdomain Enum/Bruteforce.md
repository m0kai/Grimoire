-- -
Contains enumeration for subdomains, mostly this goes over virtual host fuzzing as it is the more likely thing you will be enumerating. You can get classic subdomain information from [[Dark Arts/Recon/OSINT/DNS|DNS]] enumeration and the like, but for fuzzing you will most likely be fuzzing virtual hosts. 
### dnsenum
Bruteforce subdomains. Basically the same as using ffuf, in this case, the wordlist used is from #seclists
```bash
# -r: recursive, checks subdomains of found subdomains
dnsenum --enum <hostname> -f <wordlist> -r
dnsenum --ennm inlanefreight.com  -f /usr/share/seclists/Discovery/DNS/subdomains-top1million-5000.txt -r
```
