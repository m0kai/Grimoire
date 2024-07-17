-- -
A type of #pass-the-hash attack where you get a hash from something like [[LLMNR Poisoning]] and then relay the captured hash to another machine to potentially get access to it. 
#### Requirements
- SMB signing must be **disabled** on the **target**. 
- Relayed credentials must be local admin on the **target** machine for any real value out of it.
#### Steps
1. Find targets by identifying alive hosts w/ SMB Signing disabled
2. Setup Responder
3. Run Responder
4. Run ntlmrelayx
#### Identify Hosts w/o SMB Signing Enabled
Scan the entire network CIDR to see which machines have SMB signing disabled. 
```bash
nmap --script smb2-security-mode -p 445 10.0.0.0/24
```
#### Setup Responder
```bash
sudo mousepad /etc/responder/Responder.conf

# Make sure the following are set to off:
# SMB = Off
# HTTP = Off

# Remember to turn them back on when you're done!
```
#### Run Responder
![[Responder#^92af1e]]
#### Run ntlmrelayx
![[ntlmrelayx#^b5239c]]
