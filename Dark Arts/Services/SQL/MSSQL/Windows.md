-- -
### CLI
#### Connect to db
```powershell
# works in cmd
sqlcmd -S <ip> -U <usr> -P <passwd>
# sqlcmd, works on cmd
sqlcmd -u <user> -P '<passwd>' -y 30 -Y 30 # for "better looking" output
sqlcmd -S 10.129.20.13 -U username -P Password123
```
#### Query DB
```mysql
# you need to first input the query, then execute a GO command to actually run the query. GO command can be all caps or all lowercase.

# show databases
SELECT name FROM master.dbo.sysdatabases
GO

# Select a database
USE <db> 
GO

# Show tables
SELECT table_name FROM <db>.INFORMATION_SCHEMA.TABLES
GO

# select data from table 
SELECT * FROM <table>
go
```
### GUI
[SQL Server Management Studio (SSMS)](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16) which is a Windows-only tool.  
