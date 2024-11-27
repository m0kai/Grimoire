-- -
The default databases created to maintain the database itself. All MySQL servers will have these on there. You can enumerate info from them but will hold less sensitive information than other tables.
- `master` - keeps the information for an instance of SQL Server.
- `msdb` - used by SQL Server Agent.
- `model` - a template database copied for each new database.
- `resource` - a read-only database that keeps system objects visible in every database on the server in sys schema.
- `tempdb` - keeps temporary objects for SQL queries.