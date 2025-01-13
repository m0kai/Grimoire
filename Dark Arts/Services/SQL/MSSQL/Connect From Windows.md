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
### GUI
[SQL Server Management Studio (SSMS)](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?view=sql-server-ver16) which is a Windows-only tool.  
