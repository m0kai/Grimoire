-- -
The explanation for doing this wasn't found to be satisfactory, so do research or along the way fill in how to actually do this practically. 
#### winpeas.exe
[[Dark Arts I/File Transfer/Windows|File Transfer]] the executable over to the target box. 
```powershell
# dumps a lot of info
# looking for:
# [*] Interesting Services -non Microsoft-(T1007)
# [?] Check if you can overwrite some service binary or perform DDL hijacking, also check for unquored paths
winpeas.exe
```