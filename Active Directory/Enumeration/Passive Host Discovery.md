-- -
Passively recon the network to find targets for further enumeration.
#### wireshark / tcpdump
Put your ear to the ground and see what's on the wire for us to pick up. We can see stuff like ARP requests and MDNS that can provide context to how the environment is setup and what technology is used on the network.

With Arp requests, we can identify live hosts on the network.  With MDNS we can identify hostnames. 

**Wireshark**
![[wireshark#^dfbc1f]]

**tcpdump**
![[tcpdump#^c7551f]]
**Responder**
![[Responder#^91aa51]]