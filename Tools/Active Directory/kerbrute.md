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
```bash
# this assumes you have identified two data points:
# Domain Controller: You've identified the IP of a Domain Controller
# Domain: You know the name of the Domain administered by the Domain Controller
kerbrute userenum -d <domain> --dc <dc ip> <user wordlist> -o <output file> 
kerbrute userenum -d INLANEFREIGHT.LOCAL --dc 172.16.5.5 jsmith.txt -o valid_ad_users
```

^3c4231
