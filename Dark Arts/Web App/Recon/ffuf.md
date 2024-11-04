-- -
Various flags to use ffuf.
### Extensions
Fuzz for actual files using one or more extensions:
```bash
# note, this will also do normal directory fuzzing as well as fuzzing with file extensions. 
ffuf -u http://10.10.10.10 -w /usr/share/wordlists/dirb/big.txt -e .html,.log,.php
```