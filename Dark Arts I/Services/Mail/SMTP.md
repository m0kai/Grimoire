-- -
Simple Mail Transfer Protocol. Note that you cannot retrieve emails from SMTP, you need to go through [[POP3]] or IMAP.
### Commands/recon
Some enumeration using SMTP commands.
```bash
# connect to SMTP service
telent <ip> 25
nc -nv <ip> 25

# VRFY
# Asks mail server if the input email username is valid or not
VRFY root
VRFY www-data

# EXPN
# same as VRFY for users, but if you use a distribution list rather than a specific email username, it lists the emails that are a part of the distribution list. 
EXPN john # user
EXPN support-tem # DL

# RCPT
# identifies the recipient of the email message
RCPT TO:julio
```
### smtp-user-enum
You can automate the process of enumerating users via SMTP with this tool.
```bash
# -M: Enum Mode, could be VRFY, EXPN, or RCPT. May have other modes.
# -U: userlist
# -D: domain (@gmail.com), may or may not be necessary
# -t: target IP
smtp-user-enum -M <mode> -U <userlist> -D <domain> -t <ip>
smtp-user-enum -M RCPT -U userlist.txt -D inlanefreight.htb -t 10.129.203.7
```
### Look for SMTP Open Relay Servers
can be leveraged in a phishing campaign. It would allow us to send emails to employees that come from legitimate source emails so they are likely to trust it and click our malicious link. 
```bash
# enum if the server/service is setup as an Open Relay
nmap -p 25 -Pn --script smtp-open-relay

# from here you can connect to the open relay server using any email client you wand and just fill in the info and message you desire. 
# For example:
swaks --from <source email acct> --to <dl> --header <subject line> --body <email message w/ malicious link> --server <ip of open relay server> 

swaks --from notifications@inlanefreight.com --to employees@inlanefreight.com --header 'Subject: Company Notification' --body 'Hi All, we want to hear from you! Please complete the following survey. http://mycustomphishinglink.com/' --server 10.10.11.213
```