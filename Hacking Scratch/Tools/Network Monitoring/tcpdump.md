-- -
Network monitoring tool, but on the CLI. Great for situations where you only have CLI access to a machine.

*Note: You can save the output to a pcap file and then transfer the pcap to a system you have GUI access to and open it in [[wireshark]].*
#### Basic Usage
```bash
# You can save the output to a pcap file and then transfer the pcap to a system you have GUI access to and open it in wireshark.
sudo tcpdump -i <interface name>
sudo tcpdump -i ens224
```

^c7551f
