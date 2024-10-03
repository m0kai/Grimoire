-- -
Tool written in Go that you can use to create a tunnel via SSH to forward your traffic through.
### Install
```bash
# on attack host
# Make sure Golang is installed on your system
git clone https://github.com/jpillora/chisel.git
cd chisel
go build
```
### Transfer binary
```bash
# scp chisel binary from attack host to pivot host
scp chisel ubuntu@10.129.202.64:~/
```
### Run Server
```bash
# on pivot host
./chisel server -v -p 1234 --socks5
```
### Run Client
```bash
# on attack host
./chisel client -v <pivot host ip>:<server port> socks
./chisel client -v 10.129.202.64:1234 socks
```
### Config proxychains
```bash
# on attack host
# note: in the client command above, it will output the port the client is listening on, for our example it output 1080 as the local listener port
sudo vim /etc/proxychains.conf

# in /etc/proxychains.conf:
socks5 127.0.0.1 1080
```
### Forward traffic via proxychains
```bash
# run whatever you want to run via proxychains
# may or may not need sudo
proxychains xfreerdp /v:172.16.5.19 /v:victor /p:pass@123
```
### Reverse Pivot 
Use this method when restricted by a firewall with limited inbound traffic allowed. 
```bash
# Start server on pivot host
sudo ./chisel server --reverse -v -p 1234 --socks5

# start client on attack host
./chisel client -v 10.10.14.17:1234 R:socks

# edit proxychains file
sudo vim /etc/proxychains.conf

# input into proxychains config file
socks5 127.0.0.1 1080

# funnel commands through proxychains
proxychains xfreerdp /v:172.16.5.19 /u:victor /p:pass@123
```