-- -
### SSH Tunnel
-- - 
#### ProxyChains
```bash
# check proxychains config for bind port, should say something like:
# socks4 127.0.0.1 9050
cat /etc/proxychains4.conf # can be a higher number

# take that port number and bind a tunnel to it
# in this example it is port 9050
# flags:
# -f: background ssh, since it's a bind we will be using in the future
# -N, don't run commands, good for Port forwarding. 
# -D, specify port to bind to, 9050 in our case for proxy chains
# -i, specify SSH key  for auth
ssh -f -N -D <bind port> -i <ssh key> <user>@<target ip>
ssh -f -N -D 9050 -i id_rsa root@10.10.155.5

# Now the tunnel should be setup, you just need to prepend your commands with "proxychains" to send the traffic through our ssh tunnel. 
# for example:
proxychains nmap -p 88 10.10.10.225

# for nmap specifocly, you can get funky shit with nmap scans, so a tip is to do a full TCP scan rather than a stealth SYN scan
proxychains nmap 10.10.10.225 -sT
```
#### sshuttle
```bash
# install
sudo pip install sshuttle

# setup tunnel
# Look for "connected to server"
# this will then catch any request into that cidr range, and route it
# through this tunnel, so you can use commands like normal without needing to put anything in front of it like proxychains.
sshuttle -r <user>@<target ip> <cidr range> --ssh-cmd "ssh -i <ssh key>"
sshuttle -r root@10.10.155.5 10.10.10.0/24 --ssh-cmd "ssh -i id_rsa"

# then from here you can run commands like normal
nmap 10.10.155.225
```
#### chisel
[Repo](https://github.com/jpillora/chisel)