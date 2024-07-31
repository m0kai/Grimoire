-- -
Sometimes you will have stored credentials to your session. You do not need to get them cleartext to use them
##### Stored credentials on disk
```powershell
# looks for credentials that have been stored to disk/in a file?
cmdkey /list
```
If you find stored credentials, you can [[RunAs|Exploit this]]
