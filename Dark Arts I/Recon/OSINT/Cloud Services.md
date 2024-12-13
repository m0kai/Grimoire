-- -
Look for cloud resources leveraged by the company. You may find a cloud resource during research into [[Dark Arts I/Recon/OSINT/DNS|DNS]] or [[Certs]] enumeration. Will have amazonaws.com or such in the url.
### Google
A more targeted way is to use Google Dorks.
```bash
# AWS
intext:<domain> inurl:amazonaws.com

# Azure
# queries for storage blob
intext:<domain> inurl:blob.core.windows.net
```
### Resources
[domain.glass](https://domain.glass)
[GreyhatWarfare](https://buckets.grayhatwarfare.com)