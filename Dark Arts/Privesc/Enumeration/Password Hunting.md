-- -
Look through files for cleartext passwords.
```bash
# color output which may or may not be possible depending on what type of shell you have. 
# looks for the string "password" inside of files
grep --color=auto -rnw '/' -ie "PASSWORD" --color=always 2> /dev/null
grep --color=auto -rnw '/' -ie "PASSWORD=" --color=always 2> /dev/null

# looks for files with password in the filename
locate password | more
locate pass | more
locate pwd | more

# find SSH keys
find / -name id_rsa 2> /dev/null
```