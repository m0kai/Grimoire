-- -
General usage of nmap, more specific usage of nmap can be found in other locations relating to that specific usage. 
### NSE Scripts
-- -
##### Update Scripts
```bash
sudo nmap --script-updatedb
```
##### Search Scripts
```bash
# general 
find / -type f -name ftp* 2>/dev/null | grep scripts

# more specific I think
find /usr/share/nmap/scripts -type f -name <service>* 2>/dev/null | grep scripts
```
##### Trace
Trace steps the script takes for debugging or getting more verbose data 
```bash
nmap -sV -sC -A 10.10.10.10 --script-trace
```
