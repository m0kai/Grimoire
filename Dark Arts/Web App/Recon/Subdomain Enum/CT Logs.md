-- -
Certificate Transparency (CT) Logs are public, append-only logs that record historic issuance of SSL/TLS certs. Independent organisations maintain these logs, and it is multiple organisations, not just one. The logs are also public, so they are monitored by the orgs as well as security researchers, engineers, etc. This is an attempt to try to validate certificates and cut down on falsified/malicious certs. 

With this historic data, you can search for subdomains in the history of these logs for potentially active or forgotten subdomains. Classifies under #OSINT imo
### crt.sh
[Web Interface](https://crt.sh)
```bash
# Use curl, api, and bash-fu to get list of subdomians w/ dev in the name
curl -s "https://crt.sh/?q=<host>&output=json" | jq -r '.[] | select(.name_value | contains("dev)) | .name_value' | sort -u
```
### Censys
[Web Interface](https://search.censys.io)