-- -
Try to log into multiple accounts with one password, so roll through a wordlist of usernames trying a single password, or a small list of passwords, for each username. This technique is common in AD since there will be a password policy that's enforced and there will be a password lockout policy to stop standard bruteforce attacks. 
### TTP
1. Try to get the organization's [[Hacking Scratch/Active Directory - HTB/Enumeration/Password Hunting/Password Policy]]
2. Build a list of valid [[Username Enumeration (unauth)|usernames]]
3. Come up with spray plan (how many attempts over what time period and with a delay)
4. Spray within the plan
## Attack
### From Linux
#### rpcclient
![[Hacking Scratch/Tools/Active Directory/Linux/rpcclient#^c36a7d]]
#### kerbrute
![[Hacking Scratch/Tools/Active Directory/Linux/kerbrute#^ab0bcd]]
#### crackmapexec
###### Domain-level Password spray
This will password spray AD accounts
![[Hacking Scratch/Tools/Active Directory/Linux/crackmapexec#^4d0ec2]]
###### Local Password Spray
This will password spray for local accounts on the systems in the IP range specified
![[Hacking Scratch/Tools/Active Directory/Linux/crackmapexec#^cc2b19]]
### From Windows
