-- -
Search for exposed systems on the public internet. 
### Shodan
Show systems that are publicly accessible to the internet. This includes websites, servers, IoT devices, security cameras, webcams, etc.
In this workflow, generate a subdomain list w/ IPs using [[Certs|crt.sh]]
```bash
# the subdomainlist file is a file of subdomains generated from crts.sh or some other method.
# first generate an IP list from the subdomains
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f4 >> ip-addresses.txt;done

# then, use ip list to query Shodan
for i in $(cat ip-addresses.txt);do shodan host $i;done
```