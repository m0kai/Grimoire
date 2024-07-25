-- -
You know what nmap is for. 
### Basic Usage
```bash
# -iL: take in list of targets
nmap -iL hosts.txt

# -oA: output findings to all formats
nmap 10.10.10.10 -oA scans
```