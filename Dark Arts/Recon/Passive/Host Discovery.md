-- -
For when you find yourself on a network blind. You will passively `put your ear to the wire` and just sniff packets out of the air to derive alive hosts and such on the network. 
### TCP Dump
-- -
For instances where you only have a CLI and no GUI, or if you like this more.
```bash
sudo tcpdump -i <interface>
sudo tcpdump -i ens224 
```
### Responder
-- -
You obviously use responder for other useful shit, but it can sniff traffic off the wire and display the info, fulfilling the passive recon and host discovery function.
```bash 
sudo responder -I <interface> -A
sudo responder -I ens224 -A 
```
### Wireshark
-- -
You can just start wireshark on the NIC connected to the network and pick up alive hosts, IPs, hostnames, etc. 
```bash
# from the CLI
sudo -E wireshark
```
##### ARP Packets
In the output, you can filter `arp` and see the ARP packets flying around. Say you see an arp packet that says: 
`Who has 172.16.5.1? Tell 172.16.5.50`
Then you can derive that an alive host is at `172.16.5.50`, and potentially there is an alive host at `172.16.5.1`. 
![[Pasted image 20241212110028.png]]
##### MDNS 
You can filter by MDNS which should reveal alive hostnames on the network. Since you are getting the DNS responses for the said hostnames, finding the corresponding IP should be as simple as asking dns for it in an `nslookup` or `ping` command.
![[Pasted image 20241213073648.png]]