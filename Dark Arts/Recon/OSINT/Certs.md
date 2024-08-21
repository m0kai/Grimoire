-- -
SSL Certificates can hold domain information. More specifically subdomains that are likely still valid if they are in their certificates for a company's domain. 
### crt.sh
[Web UI](https://crt.sh)
```bash
# Curl
# get output as json and parse for pretty output
curl -s https://crt.sh/\?q\=inlanefreight.com\&output\=json | jq .
curl -s "https://crt.sh/?q=<domain>&output=json" | jq .

# output and parse for only subdomains
curl -s https://crt.sh/\?q\=inlanefreight.com\&output\=json | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u

curl -s "https://crt.sh/?q=inlanefreight.com&output=json" | jq . | grep name | cut -d ":" -f 2 | grep -v "CN=" | cut -d '"' -f 2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u

# Get subdomains that are publicly avaialable and are not hosted by third-party providers. We cannot hack sites hosted by third party providers without getting consent from the third party provider.
# sudomainlist would be the output from above command(s).
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f1,4;done
```