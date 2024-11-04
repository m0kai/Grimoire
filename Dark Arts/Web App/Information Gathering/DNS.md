-- -
### Dig
```bash
dig domain.com
dig domain.com A
dig domain.com AAAA
dig domain.com MX
dig domain.com NS
dig domain.com TXT
dig domain.com CNAME
dig domain.com SOA
dig @<name server> domain.com
dig +trace domain.com
dig -x 192.168.1.1 # reverse dns lookup, ip -> hostname
dig +short domain.com
dig +noall +answer domain.com
dig domain.com ANY
```
### Dig - Zone Transfer
```bash
dig axfr @<name server> <domain>
dig axfr @nsztm1.digi.ninja zonetransfer.me
```