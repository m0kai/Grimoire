-- -
Connect to other MSSQL server/instances. A way to move laterally from a MSSQL perspective. You may have linked servers where you can connect to them and their DB from your current MSSQL instance.
### Identify Linked Servers
```mysql
# 1 is a remote server
# 0 is a linked server
# I assume this to mean 1 is a server on a remote system and a 0 is a linked server that is actually another instance on the same system you are on...I think...
SELECT srvname, isremote FROM sysservers
GO
```
### Run query on remote server DB
```mysql
# If quotes are needed in the query, use a sinle quote to escape the single quote
# To run multiple queries at once, separate queries by a semicolon
EXECUTE('select @@servername, @@version, system_user, is_srvrolemember(''sysadmin'')') AT [10.0.0.12\SQLEXPRESS]
```