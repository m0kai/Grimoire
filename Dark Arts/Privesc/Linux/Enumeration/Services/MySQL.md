-- -
various ways to see if #mysql is vulnerable. 
### User Defined Function privesc
Couldn't find a CVE attached to this. mysql is vulnerable if the service is running as root w/o a password and the version is `4.x` or `5.x`.
```bash
# looking for root
ps aux | grep mysql

# check the version
# Will output something like: 
# mysql  Ver 14.14 Distrib 5.1.73, for debian-linux-gnu (x86_64) using readline 6.1
# which in this example means mysql is version 5.1.73
mysql --version

# try to login to mysql root user without password
mysql -u root

# it should let you login without providing a password, and spit out:
# Server version: 5.1.73
# which confirms the vulnerable mysql version.
```
From here, [[Dark Arts/Privesc/Linux/Exploits/Services/MySQL|exploit]]
*Note: This may still work if you need the mysql root password and it isn't just empty!*