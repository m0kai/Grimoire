-- -
Enumerating data about the users on the system. 
##### Your current user
```powershell
# get your user
whoami

# your privs
whoami /priv

# groups you are a part of
whoami /groups
```
##### Other users on the system
```powershell
# pull info on other users like group memebership
net user <username>
net user administrator
```
#### groups
```powershell
# all groups on system, may or may not work
net localgroup

# specific groups
net localgroup <group name> 
net localgroup administrators
```