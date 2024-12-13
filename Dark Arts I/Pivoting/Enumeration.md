-- -
### NICs
Check if the system is dual homed, i.e. has 2+ NICs connecting it to multiple subnets. 
```bash
# using more modern ip
ip a
ip addr

# older ifconfig
ifconfig
```
### Routing
You may need to route traffic manually, so checking the routing table may be helpful
```bash
netstat -r 
```