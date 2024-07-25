-- -
Can be used for a multitude of things, but I will likely only be using it to discover alive hosts on a network with a ping sweep. 
#### Host Discovery
```bash
#-a: show targets that are alive
# -s: print stats at the end of the scan
# -g: generate a target list from the provided CIDR network
# -q: Do NOT show per-target results
fping -asgq 172.16.5.0/23
```

^bac9e3
