-- -
Get info about yourself and the other users on the system.
#### You
Information about the user you are currently logged in as/have a shell as
```bash
# you username
whoami

# groups you are in, your user ID on the system, etc
# key groups: 
# docker, lxd, root
id

# usually a dead end, but you may find sensitive info you user input into their terminal here.
history
```
#### Sudo
enumerate your sudo privs. If you find something you can sudo, you may be able to exploit it to elevate privileges depending on what the software is and what the sudo rights are. 
```bash
# may or may not require a password, so try no matter the shell.
sudo -l
```
If you have sudo rights to something, go [here](https://gtfobins.github.io/#+sudo)
#### Other Users
```bash
# at bare minimum shows all the other users on the system. At best, you can find a password hash in here.
# root at top, actual users at the bottom.
cat /etc/passwd

# output only usernames
cat /etc/passwd | cut -d : -f 1
```
#### Sensitive User files
```bash
# if you can do the following then you can unshadow the passwords and then proceed to crack
cat /etc/shadow

cat /etc/groups
```