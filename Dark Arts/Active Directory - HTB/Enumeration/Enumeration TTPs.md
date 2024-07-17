-- -
#### Key Data Points

| **Data Point**                  | **Description**                                                                                                     |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `AD Users`                      | Looking for Targets for password spraying                                                                           |
| `AD Joined Computers`           | Looking for key systems such as Domain Controllers, file servers, Database servers, web servers, mail servers, etc. |
| `Key Services`                  | Looking for AD services such as Kerberos, NetBIOS, LDAP, DNS                                                        |
| `Vulnerable Hosts and Services` | Anything that can be a quick win. An easy host to exploit and gain a foothold.                                      |
#### Steps
1. [[Passive Host Discovery]] of any hosts on the network
2. Active validation of the results & further enumeration 
	- nmap scan to verify hosts are alive
	- nmap scan for open ports
	- Identify services running on open ports
	- Identify vulnerabilities
3. Regroup, go over results
	- Identify lowest hanging fruit
	- Identify possible quick wins
	- Prioritize hosts based on probability of quick win
	- Remember key point is that you are looking for initial or further AD access, user accounts are highest priority, even if just a username. 
4. [[Username Enumeration (unauth)|Bruteforce Valid Usernames]]
	- Will require you know the IP of the DC
	- Will require you know the Domain (e.g. INLANEFREIGHT.LOCAL)