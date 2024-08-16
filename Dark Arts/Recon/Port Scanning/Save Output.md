-- -
[Docs](https://nmap.org/book/output.html)
- `-oN`: normal output, puts what you see in stdout to a file
- `-oG`: Grepable output, output that can easily be grep'd
- `-oX`: XML output
- `-oA`: Output all of the above into separate files
### XML->HTML
Useful for reporting and showing results to non-technical people.
```bash
# output scan to XML
nmap 10.10.10.10 -oX target.xml

# convert output XML to HTML
xsltproc target.xml -o target.html
```
