-- -
### Linux
-- -
#### Null Session Listing
```bash
# list out available shares and log in with a null session
smbclient -N -L //10.10.10.10
```
#### Connect to Share
```bash
# default domain: WORKGROUP
# default user: your computer username
# will ask for password
smbclient //10.10.10.10/notes
```
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
### Windows
-- -
#### GUI
If you have RDP access, or access to physical windows machine, you can use `[WINKEY] + [R]` then type in the share location, for example, `\\192.168.220.133\Finance\` and it should open a file explorer window of the share. This connects automatically if anonymous access is allowed or if the user you are logged in as has permissions to mount the share, otherwise it will ask you to authenticate. 
#### CLI
##### CMD
```powershell
# connect to share and mount it to a letter drive, in our example the n:\ drive.
net use <local drive> \\<ip>\<share>
net use n: \\192.168.220.129\Finance

# using authentication creds
net use <drive letter> \\<ip>\<share> /user:<user> <passwd>
net use n: \\192.168.220.129\Finance /user:plaintext Password123

# from here just interact with the share as you would anything else on the local system. 
```
##### PowerShell
```powershell
# dir share
Get-ChildItem \\<ip>\<share>\
Get-ChildItem \\192.168.220.129\Finance\

# mount share locally
New-PSDrive -Name "<drive letter>" -Root "\\<ip>\<share>" -PsProvider "FileSystem"
New-PSDrive -Name "N" -Root "\\192.168.220.129\Finance" -PSProvider "FileSystem"

# Mount w/ Creds
$username = "plantext"
$password = "Password123"
$secpassword = ConvertTo-SecureString $password -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential $username, $secpassword
New-PSDrive -Name "N" -Root "\\192.168.220.129\Finance" -PSProvider "FileSystem" -Credential $cred
```