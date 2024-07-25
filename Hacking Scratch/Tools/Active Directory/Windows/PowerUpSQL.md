-- -
#### Enum MSSQL
```powershell
cd .\PowerUpSQL\
Import-Module .\PowerUpSQL.ps1
Get-SQLInsctanceDomain # gets instances data about the server

# Run authenticated mssql query on remote host
Get-SQLQuery -Verbose -Instance "<ip>" -username "<domain>\<user>" -password "<password>" -query '<mssql query>'

Get-SQLQuery -Verbose -Instance "172.16.5.150,1433" -username "inlanefreight\damundsen" -password "SQL1234!" -query 'Select @@version'
```

^b601b7
