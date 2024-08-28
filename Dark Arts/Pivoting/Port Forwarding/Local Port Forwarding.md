-- -
This section is for situations where you have a service bound to a port, but that service and port are only accessible from within the server. So you can only access it from localhost on the target host. 
For example, if you scan a target and port 3306 (MySQL) shows up as closed in the nmap scan, but you get onto the server and you see mysql is running and you can access it from a shell on the server. This means its locally hosted, it **can** be accessed **locally**, but **cannot** be accessed **remotely**. 
To run exploits against it that are remote in nature, you can bind a local port on your attack box to the local mysql port on the target box through SSH, if you can authenticate to SSH of course:
```bash
# single port
ssh -L <local port>:localhost:<target local port> <user>@<ip>
ssh -L 1234:localhost:3306 ubuntu@10.129.202.64

# multiple ports
ssh -L 1234:localhost:3306 -L 8080:localhost:80 ubuntu@10.129.202.64
```
Then, you can nmap the local port you bound the target local port to:
```bash
nmap -p 1234 localhost
```
