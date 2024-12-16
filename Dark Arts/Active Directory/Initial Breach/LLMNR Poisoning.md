-- -
Same process for #NBT-NS and #MDNS poisoning. Basic explanation is that LLMNR is the fallback for when DNS fails to resolve something. When a network resource (ip, share, etc) is requested and DNS fails to resolve and IP for that resource, the computer will fallback to LLMNR and broadcast out a request looking for said resource by asking each item in the network if it is the requested resource. We can setup responder or whatever to sit and wait for this broadcast request to come in, when it does, we don't care what the request is for, we tell it that we are requested resource and require authentication from the requester. This should then give us a username and a NTLM hash of their password. If we can crack the password, it can be a quick way to get into the AD network initially. 
### TTPs
- Leave running throughout the normal workday (9-5).
- Focus on times where people will be first logging in, i.e. in the morning around 9am, then again at around 13:00 when they would be returning from lunch. 
#### Attack
[[LLMNR, NBT-NS, & MDNS Poisoning]]
![[Responder#^92af1e]]
**Then Crack the hash**
```bash
hashcat -m 5600 hash /usr/share/wordlist/rockyou.txt -O 
```
All saved logs can be found at: `/usr/share/responder/logs`