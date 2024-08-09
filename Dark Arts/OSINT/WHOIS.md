-- -
query-response protocol designed to access databases that store information about registered internet resources. Phonebook of the internet, because I'm definitely old enough to make that association. They harp on this information being valuable, but I have yet to a find it useful at all. 
##### Usage
```bash
whois <domain>
whois inlanefreight.com
```
###### Records primarily hold:
- Domain name - `inlanefreight.com`
- Registrar - Company where domain was registered: `GoDaddy`, `Namecheap`, etc
- Registrar Contact - Persons/Org that registered the domain
- Administrative Contact - Person responsible for managing the domain
- Technical Contact - Person handling technical issues related to the domain
- Creation and Expiration Dates - when the domain was registered and expires
- Name Servers - Servers that translate that domain name into an IP
- IP address blocks - Address blocks reserved to domain
###### Use Cases
- Identify Key Personnel
	- Names, email, and phone numbers of individuals responsible for managing the domain. 
	- Info can be leveraged for social engineering attacks
- Discover Network Infrastructure
	- Name Servers and IPs provide clues about target network infrastructure. 
	- Help identify entry points/misconfigurations
- Historical Data Analysis
	- Reveal ownership, contact information or technical details over time. 
	- Track evolution of target's digital presence