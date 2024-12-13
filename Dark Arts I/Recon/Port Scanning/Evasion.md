-- -
Get past firewalls, IPS, and IDS. 
### Using decoys
```bash
# sends packets from 5 random IP addresses, real IP is placed in one of the 5 different IPs at random. 
sudo nmap 10.10.10.10 -D RND:5
```
### Specify Interface
```bash
 # send packets through a speicific interface
 sudo nmap 10.10.10.10 -e tun0
```
### DNS Proxy
```bash
# send your packets out from tcp port 53 so that firewalls/IDS/IPS get tricked into thinking the packets are from a DNS server and thus are let through
sudo nmap 10.10.10.10 --source-port 53
```