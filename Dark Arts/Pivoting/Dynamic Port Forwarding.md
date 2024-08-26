-- -
Dynamically forward ports instead of statically specifying a port. You forward all traffic to 1 port which in turn will forward traffic across the segmented network. 
### Proxychains
-- -
This workflow is called SOCKS tunneling. 

Things to note:
- You can only perform `full TCP connect scans` over proxy chains
- `host-alive` checks may not work against windows targets bc Windows Defender firewall blocks ICMP requests (traditional pings) by default. 
### Setup
verify/edit `/etc/proxychains.conf` to have the following line, usually already present in config:
```bash
socks4 127.0.0.1 9050 # port number is irrelevant
```
Then, setup SSH proxy:
```bash
# userpass auth
# port matches what you set in proxychains.conf
ssh -D <port> <user>@<ip>
ssh -D 9050 ubuntu@10.129.202.64

# private key auth
ssh -D 9050 ubuntu@10.129.202.64 -i "id_rsa"
```
### Usage
```bash
# it seems like you may need to sudo proxychains to get it to work
# may only work to get nmap working, and I was able to RDP without it on the internal machine, so idk. 
sudo proxychains <command> 

# -------- nmap --------
# host discovery
# skip port scan, will likely not show windows targets
sudo proxychains nmap -v -sn 172.16.5.1-200

# Valid scan against windows target
# key flags:
# -sT: Full TCP connect scan
# -Pn: skip host-alive (ping) check
proxychains -v -Pn -sT 172.16.5.19

# -------- msfconsole --------
proxychains msfconsole

# -------- xfreerdp --------
proxychains xfreerdp /v:172.16.5.19 /u:victor /p:pass@123
```
### troubleshooting
Proxychains (and others) seems to be a bitch at times about how you get it to work. Through the HTB module and playing with pivoting, I found that even if something like `nmap` isn't working, you can still access a port if you know it's open.

For example, the exercise was to RDP into an internal machine through proxychains and your pivot machine. I wasn't able to scan it with nmap, but since I knew RDP was open, I used `proxychains xfreerdp`, and I was able to log into the machine.

Through playing with proxychains, I was finally able to get nmap to work by using sudo with proxychains and forcing the full TCP connect scan, so the following is **required** to get TCP scans and nmap working through proxy chains:
```bash
sudo proxychains nmap -Pn -sT <ip addr> <other flags> 
```