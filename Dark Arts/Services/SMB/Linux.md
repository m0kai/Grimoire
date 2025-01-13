-- -
### netexec
[[Dark Arts/Tools/Netexec|Netexec tool page]]
![[Enum SMB Shares#^b3c92f]]
#### Mount Share
Install:
```bash
sudo apt install cifs-utils
```
Mount: 
```bash
# make a mount location
sudo mkdir /mnt/<location>
sudo mkdir /mnt/Finance

# mount share to created location
sudo mount -t cifs -o username=<user>,password=<password>,domain=<domain> //<ip>/<share> /mnt/<location>
sudo mount -t cifs -o username=plaintext,password=Password123,domain=. //192.168.220.129/Finance /mnt/Finance

# alternatively, use a credentials file
mount -t cifs //<ip>/<share> /mnt/<location> -o credentials=<path to creds file>
mount -t cifs //192.168.220.129/Finance /mnt/Finance -o credentials=/path/credentialfile
```
Credentials file would look like:
```bash
username=plaintext
password=Password123
domain=.
```
#### Download Files
```bash
get <file> 
```