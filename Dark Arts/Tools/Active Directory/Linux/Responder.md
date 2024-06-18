-- -
Used to monitor network traffic, and more interestingly, to poison `LLMNR`, `NBT_NS` and `MDNS` packets.
### Basic Usage
**Passive Recon of network**
```bash
# monitor traffic passively
# -A: Analyze mode, just pick up what's on the wire but don't poison anything.
sudo responder -I <interface> -A
```

^91aa51

**Poison LLMNR/NBT_NS/MDNS**
```bash
# note that sudo is required to access the standard ports used by Responder to poison requests. 
sudo responder -I ens224 
```

^92af1e

### Logging
Responder puts out the hashes it gets onto stdout, but it will also save the results to its logs. 

The logs can be found at the location: `/usr/share/responder/logs` 
The log file will be names as follows: `(MODULE_NAME)-(HASH_TYPE)-(CLIENT_IP).txt`
For example: `/usr/share/responder/logs/SMB-NTLMv2-SSP-172.16.5.25`
### Config
Config file can be found at the location: `/usr/share/responder/Responder.conf`
