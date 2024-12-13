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
### Bounce Attack
Not likely you will find on a modern FTP server. In essence, a relay attack. You connect to an FTP server, bounce commands from it to a second internal server, get back info from the second internal server. 
`attack box -> FTP Server -> target`
`attack box <- FTP Server <- target`
```bash
nmap -Pn -v -n -p80 -b <user>:<passwd>@<ftp ip> <target ip>
nmap -Pn -v -n -p80 -b anonymous:password@10.10.110.213 172.17.0.2
```