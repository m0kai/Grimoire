-- -
Basic usage of FTP
### Listing Contents
```bash
# basic 
ls 
dir 

# list all contents of server recusively
ls -R 
```
### Download Files
```bash
get <file> 

# from bash, download all files
wget -m --no-passive ftp://anonymous:anonymous@<ip> 
```
### Upload Files
```bash
put <file> 
```