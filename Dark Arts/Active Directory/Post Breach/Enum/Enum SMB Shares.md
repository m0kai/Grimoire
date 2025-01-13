-- -
You can do a fair amount of automated enumeration of available shares, your user's level of access to those shares, and the contents of the shares all from #netexec .
### Enum
```bash
# may (or may not) need sudo
# point to a target server, doesn't even need to be part of the domain.

# spits out the shares on the system as well as our user's permissions on each share location.
sudo netexec smb <ip> -u <user> -p <passwd> --shares

# spider through a specific share on a server. Returns the contents of the share i.e. files and folders and recursively goes through the folders. Basically spits out the full contents of the share.
sudo netexec smb <ip > -u <user> -p <passwd> -M spider_plus --share '<share>'
sudo crackmapexec smb 172.16.5.5 -u forend -p Klmcargo2 -M spider_plus --share 'Department Shares'

# resulting json with the output of above command(s) are located at:
/tmp/cme_spider_plus/<ip of host> 
```

^b3c92f
