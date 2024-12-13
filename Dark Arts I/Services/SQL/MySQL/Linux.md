-- -
#### CLI
Connect to #MySQL DB through a terminal:
```bash
# will ask for the password after you hit enter. In this way, the password is not saved as cleartext in ".bash_history" or the "history" command:
mysql -u <username> -p

# pass the password in the command, again this will save the password as cleartext in various history locations:
mysql -u <username> -p<password>

# connect to remote DB
# default port is 3306
mysql -u <username> -h <hostname or ip> -P <port> -p
mysql -u root -h docker.hackthebox.eu -P 3306 -p
```
### GUI
[MySQL Workbench](https://dev.mysql.com/downloads/workbench/)