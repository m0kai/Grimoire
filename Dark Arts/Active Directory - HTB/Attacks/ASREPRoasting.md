-- -
Similar to kerberoasting, but we are targeting AS-REP rather than TGS-REP. This attack does not require authenticated acces #noauthreq
#### Enumerating
We are looking for accounts that do not require #Kerberos preauthentication. Using #PowerView, we can get the accounts with their UAC vlaue set to `DONT_REQ_PREAUTH`.
![[PowerView (depricated)#^196ccc]]
#### Get AS-REP ticket for offline cracking
![[Rubeus#^454f39]]
**Desired hash output should look something like:**
```
$krb5asrep$23$mmorgan@INLANEFREIGHT.LOCAL:D18650F4F4E0537E0188A6897A478C55$0978822DEC13046712DB7DC03F6C4DE059A946485451AAE98BB93DFF8E3E64F3AA5614160F21A029C2B9437CB16E5E9DA4A2870FEC0596B09BADA989D1F8057262EA40840E8D0F20313B4E9A40FA5E4F987FF404313227A7BFFAE748E07201369D48ABB4727DFE1A9F09D50D7EE3AA5C13E4433E0F9217533EE0E74B02EB8907E13A208340728F794ED5103CB3E5C7915BF2F449AFDA41988FF48A356BF2BE680A25931A8746A99AD3E757BFE097B852F72CEAE1B74720C011CFF7EC94CBB6456982F14DA17213B3B27DFA1AD4C7B5C7120DB0D70763549E5144F1F5EE2AC71DDFC4DCA9D25D39737DC83B6BC60E0A0054FC0FD2B2B48B25C6CA
```
#### Cracking w/ hashcat
![[Dark Arts/Tools/Passwords/Hashcat#^364f87]]
### Kerbrute
You can also do this automatically with #crackmapexec and a valid userlist
![[kerbrute#^38353d]]
This will automatically retrieve the AS-REP hash ready to crack with #hashcat, shown above. 
### GetNPUsers
You can also do this automatically with #GetNPUsers and a userlist. The output will spit out the AS-REP hash ready for cracking in #hashcat, show above.
![[GetNPUsers.py#^ca377d]]
