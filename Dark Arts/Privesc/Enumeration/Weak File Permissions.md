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
