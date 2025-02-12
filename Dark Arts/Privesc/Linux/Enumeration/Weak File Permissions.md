-- -
#### Weak shadow file permissions
```bash
# you shouldn't be able to read the /etc/shadow unless you are root, so if you can read it then you can unshadow it and then crack the hashes for all users on the system. 
# check permissions directly
ls -la /etc/passwd
ls -la /etc/shadow

# Check you can dump /etc/shadow
cat /etc/passwd
cat /etc/shadow

```

^52dfd9

[[Abuse Shadow File|Exploit]] from here

#### Weak passwd file permissions
In some cases, the `/etc/passwd` file is writable and depending on the linux version, it may allow you to store a hash in it, allowing you to put a new password hash for root and log into it, or add a user with root permissions to the end of the file then get root that way. 
```bash 
ls -la /etc/passwd
```
