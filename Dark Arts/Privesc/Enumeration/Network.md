-- -
Enumerate the various network data present on the target. Two key points: Are there any ports open accessible to only the host, and is the system a part of multiple networks you can use to pivot?
```bash
# list network interfaces
ifconfig
ip a

# routes
route
ip route

# arp tables
arp -a 
ip neigh

# identify open ports
netstat -ano
```
#ifconfig #ip #arp #netstat 