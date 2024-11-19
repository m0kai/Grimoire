-- -
PtT attack from a Linux host. Note that a Linux system does not need to be domain joined to use kerberos tickets. It can do so for scripts or network authentication. 
### Check if system is domain joined
Need the tool `realm`
```bash
# use builtin tools
ps -ef | grep -i "winbind\|sssd"

# use specialized tools
realm list
```
### Find Keytab Files
The extension is not required to be `.keytab`, but it usually is based on convention.
```bash
# must have r/w privs to use it
find / -name *keytab* -ls 2>/dev/null
```
### Find ccache file
```bash
ls /tmp 
env | grep -i krb5
```