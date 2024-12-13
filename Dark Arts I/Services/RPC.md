-- -
### Connect via  Null Session
```bash
rpcclient -U "" 10.10.10.10
```
### Basic Usage
```bash
srvinfo
enumdomains
querydominfo
netshareenumall
netsharegetinfo <share>
enumdomusers
queryuser 0x3e9 # user rid
querygroup 0x201 # group rid
```
### Bruteforce user RIDs
```bash
for i in $(seq 500 1100);do rpcclient -N -U "" 10.129.14.128 -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done
```