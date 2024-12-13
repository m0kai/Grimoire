-- -
### Specifying Src Port
```bash
# specify what your source port should be. Used for evasion tactics.
# for example, you may want to set your source port to 53 so that any defensive measures are tricked into thinking your traffic is coming from a DNS server and thus it is implicitly trusted.
nc -nv --source-port 53 10.10.10.10 50000
```