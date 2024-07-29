-- -
#### Check user history for passwords
directly looking for passwords, but can also give you hints as to other activity the user was doing that may lead to another vector. Can show you interesting programs or workflows that you can abuse by following. For example, you can find a login for root into mysql, so that give you a mysql login, but it's also possible that the password to log into mysql is the same as the password to log into root, so try using that same password to log into the OS as root.
```bash
# not likely, but very well possible
history
histoy | grep pass 
cat .bash_history # from someone's /home directory
```
#### Search Files for cleartext passwords
Look through files in filesystem for cleartext passwords.
```bash
# color output which may or may not be possible depending on what type of shell you have. 
# looks for the string "password" inside of files
grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null
grep --color=auto -rnw '/' -ie "PASSWORD=" --color=always 2> /dev/null

# looks for files with password in the filename
locate password | more
locate pass | more
locate pwd | more

# finds password in files in pwd (current working directory)
find . -type f -exec grep -i -I "PASSWORD" {} /dev/null \;
```
#### Specific files
Files you may not think are valuable, but totally can be
```bash
# ovpn files can point to authentication files that can hold cleartext passwords.
cat myvpn.ovpn

# inside you find something like:
# auth-user-pass /etc/openvpn/auth.txt
cat /etc/openvpn/auth.txt

# then you can see a cleartext user-pass combo
```
#### Resources
- [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings)