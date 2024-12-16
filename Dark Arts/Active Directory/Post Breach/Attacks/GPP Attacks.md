-- -
Group Policy Preferences Attack. Also known as cPassword attack. Group Policy Preferences allowed admins to create policies using embedded credentials. The credentials were encrypted and placed in the `cPassword` field of the Groups.xml file on the DC. It is hosted on a share accessible to any domain user. Their is one encryption key used on every deployment of AD and it was the same across the board. The key got leaked, so the key is publicly available to everyone. Patched in #MS14-025 but that doesn't fix previous deployments. 
#### Manual
1. log into DC's `SYSVOL` share as any domain user.
2. Look through share for `Groups.xml`
3. Inside `Groups.xml`, look for `cPassword` field
4. Decrypt:
```bash
gpp-decrypt <encrypted cPassword str> 
```
#### Automated
[[Dark Arts/Active Directory/Post Breach/Tools/Attacks/metasploit]]
![[Dark Arts/Active Directory/Post Breach/Tools/Attacks/metasploit#^030f63]]
#### Mitigation
- Patch, fixed in KB2962486
- Delete old GPP XML files stored in the `SYSVOL` share of the DC.