-- -
### CLI
When the SQL server is using Windows Authentication (via local windows auth or AD), if you do not supply a domain, then it will fallback to checking its database for your credentials. If you want it to use Windows Authentication, you need to include either the domain or the hostname of the server. 
```bash
sqsh -S <ip> -U <user> -P <passwd>
sqsh -S 10.129.20.13 -U username -P Password123

# -h supresses the headers for a cleaner output
sqsh -S 10.129.203.7 -U julio -P 'MyPassword!' -h

# include domain/hostname of server, in this case a dot for the server
sqsh -S 10.129.203.7 -U .\\julio -P 'MyPassword!' -h
sqsh -S 10.129.203.7 -U WINSRV\\julio -P 'MyPassword!' -h

impacket-mssqlclient -p <port> <user>@<ip> 
impacket-mssqlclient -p 1433 julio@10.129.203.7
```
### GUI
Use [dbeaver](https://github.com/dbeaver/dbeaver). Download the release from [here](https://github.com/dbeaver/dbeaver/releases)
```bash
# assuming you are on a debian based system
sudo dpkg -i dbeaver-<version>.deb

# start the application 
dbeaver &

# then follow GUI instructions to get connected
```