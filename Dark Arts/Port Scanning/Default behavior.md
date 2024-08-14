-- -
Default behavior of #nmap depending on how you run it. 
### Defaults
- if ports are not specified, most popular 1000 TCP ports are scanned. 
- If you run it with `sudo`,  the SYN scan `-sS` is run by default
- if you **do not** run with `sudo`, the TCP scan `-sT` is run by default