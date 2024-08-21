-- -
### Basic Usage
```bash
# username password login
ssh <user>@<ip>

# using private key
ssh -i id_rsa <user>@<ip>

# allow older algorithms
# can be changed to whatever the error says when you try to use ssh normally
ssh user@10.10.209.88 -oHostKeyALgorithms=+ssh-rsa
```