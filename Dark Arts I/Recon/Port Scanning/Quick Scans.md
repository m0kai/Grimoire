-- -
Quicker scans that scan less ports than the default top 1000.
```bash
# Fast Scan
# scans top 100 ports
nmap 10.10.10.10 -F # TCP
sudo nmap -sU -F # UDP 

# specify how many top ports you want it to scan
nmap 10.10.10.10 --top-port=10
```