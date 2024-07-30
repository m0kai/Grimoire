-- -
General workflow is to find a directory you can mount that does not squash root. Mount it on your attack box, make a malicious executable as root, give malware SUID bit, then run said executable from the victim to get a shell. 
### Identify
```bash
cat /etc/exports

# in the output, you shoudl see:
# no_root_squash
# this setting will be set to a directoy, for our example it will be:
# /tmp 
# full line in /etc/exports:
# /tmp *(no_root_squash)
```
#### Verify
```bash
# from attack box
showmount -e <target ip>

# and if you see the same directory shown in /etc/exports, then this vector is open.
```
[[Dark Arts/Privesc/Linux/Exploits/NFS Root Squashing|Exploit]]
