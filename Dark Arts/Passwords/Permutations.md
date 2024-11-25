-- -
Create Custom wordlists from a base string that takes `password` and includes `Password123` and `p@$$w0rd` in the list.
```bash
hashcat --force password.list -r custom.rule --stdout > mut_password.list
```