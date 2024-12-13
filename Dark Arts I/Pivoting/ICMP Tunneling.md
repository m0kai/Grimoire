-- -
Tunnel your traffic by encapsulating it inside of ICMP packets containing echo requests and responses. Note that this only works if the environment allows ping responses. This is usually not the case. 
### Setup
```bash
git clone https://github.com/utoni/ptunnel-ng.git
cd ptunnel-ng/
sudo ./autogen.sh
```
### Alternative Setup
Not sure when/if I would need this...I ended up needing it to get this to build.
```bash
git clone https://github.com/utoni/ptunnel-ng.git
sudo apt install automake autoconf -y
cd ptunnel-ng/
sed -i '$s/.*/LDFLAGS=-static "${NEW_WD}\/configure" --enable-static $@ \&\& make clean \&\& make -j${BUILDJOBS:-4} all/' autogen.sh
./autogen.sh
```
### Transfer whole repo to pivot host
```bash
scp -r ptunnel-ng ubuntu@10.129.202.64:~/
```
### Start server on pivot host
```bash
# ip here is the ip of the pivot host the attackbox can reach, so external IP address of the pivot host
# the executable may be in the ./src folder
(ubuntu) sudo ./ptunnel-ng -r10.129.202.64 -R22
```
### Connect to ptunnel-ng server from attack host
```bash
# the executable may be in the ./src folder
sudo ./ptunnel-ng -p10.129.202.64 -l2222 -r10.129.202.64 -R22
```
### Setup dynamic port forwarding over SSH
```bash
# make sure your /etc/proxychains4.conf has the line:
# socks4 127.0.0.1 9050

# on attack host
ssh -D 9050 -p 2222 -l ubuntu 127.0.0.1
```
### Proxychains through ICMP Tunnel
```bash
proxychains nmap -sV -sT 172.16.5.19 -p 3389
```