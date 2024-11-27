-- -
#### psexec
Get a full shell, but it will create a file in the ADMIN$ share of the target and is more noticeable as every command you put in will come from the SYSTEM account, which is suspect. 
![[Hacking Scratch/Tools/Active Directory/Impacket/psexec#^d07ccd]]
#### wmiexec
Get semi-interactive shell. This will not produce a file artifact anywhere and the commands will run as a local admin user, rather than SYSTEM in the case of psexec, so this method is stealthier. 
![[wmiexec#^2a6f1f]]
