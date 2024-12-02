-- -
Tactics to use when you are trying to fuzz a parameter to an API endpoint or file or whatever.
### Wordlists
Some wordlists for you to try, in some cases you can use the same one as you would for directory fuzzing.
- `/usr/share/wordlists/dirb/common.txt` or `/seclists/Discovery/Web-Content/common.txt`
- `/seclists/Fuzzing/fuzz-bo0oM.txt`
- `/seclists/Discovery/Web-Content/burp-parameter-names.txt`
- [Arjun all default wordlists](https://github.com/s0md3v/Arjun/tree/master/arjun/db)
- [para-miner params](https://github.com/PortSwigger/param-miner/blob/master/resources/params)
- [nullenc0de's param.txt](https://wordlists.assetnote.io/)
- [Assetnote parameters_top_1m](https://wordlists.assetnote.io/) - this one is quite long
### Fuzzing
Remember that you can directly test for LFI here, and has popped up where the general fuzzing won't catch the parameter unless it has an LFI payload.
```bash
ffuf -u "http://192.168.189.80/console/file.php?FUZZ" -w ./params.txt -fs 0
ffuf -u "http://192.168.189.80/console/file.php?FUZZ=0" -w ./params.txt -fs 0
ffuf -u "http://192.168.189.80/console/file.php?FUZZ=readme" -w ./params.txt -fs 0

# LFI
ffuf -u "http://192.168.189.80/console/file.php?FUZZ=/etc/passwd" -w ./params.txt -fs 0
```