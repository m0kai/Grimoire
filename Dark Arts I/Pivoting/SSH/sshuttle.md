-- -
Pivot over SSH. Should allow you to send traffic over SSH and use nmap or RDP. 
#### Dynamic Port Forward
```bash
# in one terminal, setup sshuttle
sudo sshuttle -r <user>@<pivot ip> <pivot subnet CIDR> -v
sudo sshuttle -r ubuntu@10.129.202.64 172.16.5.0/23 -v

# then use tools like normal
nmap -v -sV -p 3389 172.16.5.19 -A -Pn
```
*Note: you may get results back from nmap as "filtered", when you can still connect to said port. For example, in practice, I got RDP back as "filtered" but was still able to connect to it via RDP. *