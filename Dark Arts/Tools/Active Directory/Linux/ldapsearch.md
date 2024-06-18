-- -
Haven't used this too much, but putting it down since it has popped up a couple of times.
#### User enum w/o valid credentials
*Note: You will need a valid LDAP serach filter*
```bash
ldapsearch -h 172.16.5.5 -x -b "DC=INLANEFREIGHT,DC=LOCAL" -s sub "(&(objectclass=user))"  | grep sAMAccountName: | cut -f2 -d" "
```

^351fbd
