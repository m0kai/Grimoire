-- -
High-level strategy for initial breach in AD. #initialcompromise 
For when you need a strategy for getting those first set of credentials to AD that allow you to dig deeper. 
### Checklist
1. Start [[Responder]] and leave it running to see if you can grab anything on the wire. Key times: start of business day (9 am) and right after lunch (13:00)
2. Run scans to generate traffic, these can be [[nmap]], nessus, etc
3. Look for websites in scope (scan for port 80, 443)
4. Look for default credentials on web portals (Printers, Jenkins, websites)
5. Run [[Dark Arts/Active Directory/Initial Breach/IPv6 DNS Takeover|IPv6 DNS Takeover]]
6. Assess [[SMB Enum|SMB]] for weaknesses, credentials, files, etc. [[SMBMap]], SMBClient, [[nmap]], metasploit
7. OSINT valid users then [[Dark Arts/Active Directory - HTB/Attacks/Password Spray|Password Spray]]
8. Fallback to traditional network pentesting, look for weak services like FTP
9. Think outside the box/try harder