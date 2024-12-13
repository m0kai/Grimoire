-- -
Used for enumerating data about the domain from a valid user account. This is information available to any domain user. Note that this is run when as part of [[Dark Arts I/Active Directory/Initial Breach/IPv6 DNS Takeover|IPv6 DNS Takeover]] when you run mitm6, so if you did that already, you already have this information. 
#### Basics
```bash
sudo ldapdomaindump ldaps://<dc ip> -u '<domain>\<user>' -p <password>
sudo ldapdomaindump ldaps://192.168.138.136 -u 'MARVEL\fcastle' -p Password1
```

^8a62f5
