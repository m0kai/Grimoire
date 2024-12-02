-- -
[Docs](https://epi052.github.io/feroxbuster-docs/docs/configuration/command-line/)
```bash
feroxbuster -u http://192.168.189.80 -w /usr/share/wordlists/dirb/big.txt -o ffuf/big_basic -t 30 -L 1 --no-recursion -x html,php
```