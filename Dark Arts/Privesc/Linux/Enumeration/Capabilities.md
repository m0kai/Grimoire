-- -
Similar vector to SUID bit being set. If capabilities are set, it will run from the perspective of root which you can then just hijack to get a shell.
```bash
# find capabilities set on programs
# looking for something like:
# /usr/bin/python2.6 = cap_setuid+ep
# 
# have also pulled it off with:
# /usr/bin/python3.6 = cap_setuid,<other shit> 
getcap -r / 2>/dev/null
```
Then go check [GTFOBins](https://gtfobins.github.io) like you would for the SUID bit.
#### Resources
- [Hacking Articles](https://www.hackingarticles.in/linux-privilege-escalation-using-capabilities/)
- [SUID v Capabilities](https://mn3m.info/posts/suid-vs-capabilities/)
- [Capabilities Privesc via OpenSSL w/ SELinux Enabled & Enforced](https://int0x33.medium.com/day-44-linux-capabilities-privilege-escalation-via-openssl-with-selinux-enabled-and-enforced-74d2bec02099)