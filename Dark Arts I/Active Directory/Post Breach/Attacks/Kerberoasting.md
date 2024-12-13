-- -
Use a valid domain #userpass to request a TGS for a service account, the ticket will include a password hash for the service account password, which we can then pivot to try to #crack to get the cleartext password then you can go back to [[Dark Arts I/Active Directory/Post Breach/Attacks/Pass Attacks|Pass Attacks]] or log into a new system or whatever.
#### GetUserSPNs
![[Dark Arts I/Active Directory/Post Breach/Tools/Attacks/GetUserSPNs#^59b305]]

#### Crack the hash
![[Dark Arts I/Active Directory/Post Breach/Tools/Hashcat#^678be7|Hashcat]]