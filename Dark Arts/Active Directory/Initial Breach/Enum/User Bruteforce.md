-- -
Enumerate valid domain users. Basically bruteforce Kerberos user authentication to get valid users on the domain.
### Kerbrute
-- -
A stealthier option, it uses kerberos pre-authentication failures that often will **not** trigger logs or alerts. For setup and install instructions, check [[Dark Arts/Tools/Kerbrute#^095548|here]].
```bash
kerbrute userenum -d <domain> --dc <dc ip> <wordlist> -o <output file>
kerbrute userenum -d INLANEFREIGHT.LOCAL --dc 172.16.5.5 jsmith.txt -o valid_ad_users
```
### Resources
- [Userlist Repo](https://github.com/insidetrust/statistically-likely-usernames)
