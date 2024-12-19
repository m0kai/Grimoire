-- -
Unauthenticated ways of enumerating the password policy.
### RPC
from Linux
```bash
rpcclient -U "" -N <ip> 
querydominfo # general domain info
getdompwinfo # get password policy info
```
### enum4linux
[[Dark Arts/Tools/enum4linux/enum4linux|tool page]]
Gets more info than just the password policy, but also tries to get the password policy
```bash
enum4linux -P <ip> 
```

^5028a6

### enum4linux-ng\
[[enum4linux-ng|tool page]]
In essence the same as enum4linux but with more features. Puts out a lot of information, but among that information is the password policy.
```bash
# outputs saved in all formats, so a json and yanl
# also prints to stdout
enum4linux-ng -P <ip> -oA <output file> 
```

^1e7c72
