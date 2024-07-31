-- -
##### General
```powershell
# list network interfaces
ipconfig

# more info on network interfaces, DNS server info
ipconfig /all

# arp tables
arp -a

# routing table
route print
```
##### Open Ports

^cc03c5

Open ports from the target server will fall into two categories:
1. **Exposed Ports** - If you see the external IP (i.e. the IP you nmap scanned), then these ports are open to everyone on the network. You should see the same ports your nmap scan picked up, but you may see some that were hidden for some reason.
2. **Locally open ports** - if you see `0.0.0.0` before the port, this shows ports that are open to localhost i.e. they are only open if accessed locally from the server itself. These may give you a new vector to attack
```powershell
# show open ports
netstat -ano
```