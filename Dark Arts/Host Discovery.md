-- -
### nmap
-- -
[Docs](https://nmap.org/book/host-discovery-strategies.html)
###### ICMP Echo (ping) based scans
```bash
# simple
nmap -sn <range>
nmap -sn 10.10.110.0/24

# without --disable-arp-ping, nmap will send an ARP request and expect a reply, marking it as "not alive" if this doesn't go through first. If it fails, the ICMP ping is not done at all, so may be work disabling the ARP ping first, and trying ONLY an ICMP ping
sudo nmap 10.129.2.18 -sn -oN host --disable-arp-ping 

# spits out only the alive IPs
# not sure sudo is needed
# -oA output all formats, -oN may be better
# Firewalls can easily block this tho
sudo nmap 10.129.2.0/24 -sn -oA tnet | get for | cud -d "" -f 5

# from hostlist file
sudo nmap -sn -oA tnet -iL hostlist.lst | grep for | cut -d " " -f 5

# multiple IPs not in a range
sudo nmap -sn -oA tnet 10.129.2.18 10.129.2.19 10.129.2.20 | grep for | cut -d " " -f 5

# sub-range
sudo nmap -sn -oA tnet 10.129.2.18-20 | grep for | cut -d " " -f 5
```
###### Debugging 
Get more details about what nmap is doing what its doing
```bash
# verbose, shows packet trace i.e. everything happening
# -PE: ICMP Echo Requests, should automatically happen when -sn is specified
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace

# --reason: nmap explains why a target is marked as "alive"
sudo nmap 10.129.2.18 -sn -oA host -PE --reason
```