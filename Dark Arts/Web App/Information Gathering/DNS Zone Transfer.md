-- -
An old vulnerability that will most likely not work on any modern DNS servers, but it is still possible to pull off and has a good payout, so worth giving it a shot. If the target DNS server is misconfigured, you may be able to get it to initiate a zone transfer, which hands you the full domain mapping and all DNS records the target server has. 
#### Dig
```bash
# You need your target server/domain, and the name server responsible for your server. 
# note: name server can be the domain controller, and often is. 
dig axfr @<target name server> <domain>
dig axfr @nsztm1.digi.ninja zonetransfer.me
```