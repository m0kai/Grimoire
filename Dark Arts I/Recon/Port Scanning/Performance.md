-- -
[Docs](https://nmap.org/book/man-performance.html)
### Timeouts
Default minimum Rount-Trip-Time (RTT) timeout is: 100ms
```bash
# lowers initial rtt timeout and sets maz timeout to 100ms, meaning a shorter rtt time, which can make the scan go faster
nmap 10.10.10.0/24 --initial-rtt-timeout 50ms --max-rtt-timeout 100ms
```
Increasing the speed may result in less detections altogether. 
### Max Retries
Default is 10
```bash
# as in, try once and if it fails do not retry that port
nmap 10.10.10.0/24 --max-retries 0
```
Again, this could lead to false negatives. 
### Parallelism
Control how many threads nmap uses
```bash
# sets maximum number of packets to be sent per second
# so this sets the max threads to 300 per second
nmap 10.10.10.0/24 --min-rate 300
```
### Timing Templates
Optimization templates. You can set these timing templates form 0-5 in varying levels of aggression. 
```bash
# -T 0: paranoid
# -T 1: sneaky
# -T 2: polite
# -T 3: normal (Default)
# -T 4: aggressive 
# -T 5: insane
nmap 10.10.10.0/24 -T 5
```