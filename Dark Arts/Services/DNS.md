-- -
Mostly enuming DNS, may add exploits as found.
### Dig
```bash
# zone transfer, for CTFs the name server is the same as the target server
dig axfr @<name server> <domain>
dig AXFR @ns1.inlanefreight.htb inlanefreight.htb
```
### fierce
Will perform DNS enum as well as a zone transfer
```bash
fierce --domain <domain>
fierce --domain zonetransfer.me
```
### subfinder
Finds subdomains using DNS, and other OSINT tools and methods
```bash
subfinder -d <domain> -v
subfinder -d inlanefreight.com -v  
```
### subbrute
brute forces DNS for subdomains
```bash
# Install
git clone https://github.com/TheRook/subbrute.git >> /dev/null 2>&1
cd subbrute
echo "ns1.inlanefreight.com" > ./resolvers.txt

# usage
./subbrute inlanefreight.com -s ./names.txt -r ./resolvers.txt
```