-- -
### Local
Before your computer goes to a public (or private) DNS server for a lookup, it uses a local file of known hosts for name resolution. On Linux and MacOS, this file is located at: `/etc/hosts`. On Windows, this file is located at `C:\Windows\System32\drivers\etc\hosts`
### Dig
Domain Information Groper
```bash
# Default A record (IPv4) lookup
dig <domain>.com
dig <domain>.com A

# AAAA record (IPv6) lookup
dig <domain>.com AAAA

# Mail Server for the domain
dig <domain>.com MX

# Identifies authoritative Name Server(s) for domain
dig <domain>.com NS

# Retreives TXT records
dig <domain>.com TXT

# Retrieves canonical name (CNAME) records
dig <domain>.com CNAME

# Retrieves Start Of Authority (SOA) recrods
dig <domain>.com SOA

# specify Name Server to query
dig @1.1.1.1 <domain>.com

# Full path of DNS resolution
dig +trace <domain>.com

# reverse DNS lookup, get a hostname from an IP address
dig -x 192.168.1.1

# Provides a short, concise answer to the query
dig +short <domain>.com

# Display only the answer section of the query
dig +noall +answer <domain>.com

# Get all available DNS records for domain
# many servers ignore ANY queries 
dig <domain>.com any
```