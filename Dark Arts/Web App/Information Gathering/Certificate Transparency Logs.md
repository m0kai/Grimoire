-- -
Basically, in order to establish trust with websites over TLS, certificates are granted to websites. There are also Transparency logs associated with every certificate that is granted to a website and its various subdomains. So if you check those logs, you can discover subdomains.
### CLI
```bash
curl -s "https://crt.sh/?q=facebook.com&output=json" | jq -r '.[]
 | select(.name_value | contains("dev")) | .name_value' | sort -u
```
### Web UI Resources
- https://crt.sh/
- https://search.censys.io/