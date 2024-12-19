-- -
Enumerate all the data from the domain. A lot of data is provided freely to any domain user, so if you have a valid AD account, you will be able to enumerate a great deal of data about the domain such as domain users, groups, and computers. You may even get lucky and see a domain user's account password in the description of the domain user. 
### General
You can get an overall view of the domain, its users, groups, and computers quickly and easily here:
##### ldapdomaindump
[[ldapdomaindump]]
Remember that if you ran mitm6, it should have output this information already.
![[ldapdomaindump#^8a62f5]]
##### Bloodhound
Graphical mind map type enumeration tool. Helps see complex or nuanced vectors based on the massive amount of data available to all domain users. Go tool page [[Bloodhound|here]].
##### Plumhound
Companion software to [[Bloodhound]]. It outputs various reports based on the domain data gathered by the [[Bloodhound]] ingestor. Another way to visually see the domain information available to all domain users. Go to tool page [[Plumhound|here]].
##### Ping Castle
Basically a vuln scanner for AD. It generates an overall security report which spits out what is wrong with the environment from a security standpoint. Used as a security audit on AD environments, but since it outputs gaps in security, you can use it to see which holes you can use to get further into the AD environment. Shows cleartext password from various places if available, such as passwords "hidden" in the description on the domain user. Tool page can be found [[Ping Castle|here]].