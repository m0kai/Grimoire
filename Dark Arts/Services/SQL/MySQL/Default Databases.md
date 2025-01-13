-- -
The default databases created to maintain the database itself. All MySQL servers will have these on there. You can enumerate info from them but will hold less sensitive information than other tables.
- `mysql` - is the system database that contains tables that store information required by the MySQL server
- `information_schema` - provides access to database metadata
- `performance_schema` - is a feature for monitoring MySQL Server execution at a low level
- `sys` - a set of objects that helps DBAs and developers interpret data collected by the Performance Schema