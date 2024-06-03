-- -
Generally used to enumerate linux information in or out of an AD context. Some common ports it uses in enumeration:

|Tool|Ports|
|---|---|
|nmblookup|137/UDP|
|nbtstat|137/UDP|
|net|139/TCP, 135/TCP, TCP and UDP 135 and 49152-65535|
|rpcclient|135/TCP|
|smbclient|445/TCP|
#### Basic Usage
```bash
enum4linux -P <ip> 
enum4linux -P 172.16.5.5
```

^43abe2

#### enum4linux-ng
Separate tool, which really is just a rewrite of the original tool in python. enum4linux-nextgeneration.
```bash
enum4linux-ng -P <ip> -oA <output files name> 
enum4linux-ng -P 172.16.5.5 -oA ilfreight
```

^68bcee

#### Generating a user lists for password spraying
```bash
enum4linux -U <ip> | grep "user:" | cut -f2 -d "[" | cut -f1 -d "]"
enum4linux -U 172.16.5.5  | grep "user:" | cut -f2 -d"[" | cut -f1 -d"]"
```

^526e0f
