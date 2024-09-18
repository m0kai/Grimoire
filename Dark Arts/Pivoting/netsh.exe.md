-- -
Windows builtin tool, can be used for a lot but this section focuses on using it to port forward. We will be opening a listening port on the dual homed pivot host on port 8080 and forward traffic to an internal host on port 3389 for RDP access.
#### Setup Port Forward
```powershell
# can be done from cmd
netsh.exe interface portproxy add v4tov4 listenport=8080 listenaddress=<external ip> connectport=3389 connectaddress=<internal target ip>

netsh.exe interface portproxy add v4tov4 listenport=8080 listenaddress=10.129.15.150 connectport=3389 connectaddress=172.16.5.25
```
#### Connect to RDP on internal host
Then just run RDP on your attack host but provide the open port on the external ip of the pivot host:
```bash
xfreerdp /v:10.129.42.198:8080 /u:victor /p:pass@123
```