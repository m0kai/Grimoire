-- -
A defense-in-depth approach will render password spray attacks extremely difficult, making it a higher barrier of entry/ require a **very** advanced **persistent** threat. 
###### Mitigation steps
- Multi-factor authentication
- Restrict access
	- Principal of least privilege
	- Only allow access to things required by the user to do their job.
- Reducing Impact of successful exploitation
	- Segmentation of the network
	- Account segmentation, as needed: admin accounts for admin tasks, user account for anything else.
- Password Hygiene
	- Good password policy
	- Restrict passwords on common wordlists
	- Restrict passwords that include the current season, month, or year
###### Detection
Ways to detect *possible* password spray attempts/events:
- Many account lockouts in a short period
- Server/application logs showing many login attempts w/ valid or non-existance users
- Many requests in a short period to a specific application, service or URL.
- DC security log events over a short period:
	- `Event ID 4625: An account failed to log on`
	- `Even ID 4771: Kerberos pre-authentiation failed` - may indicate LDAP password spraying. To monitor, need to enable Kerberos logging
- [Discussion/Research](https://www.hub.trimarcsecurity.com/post/trimarc-research-detecting-password-spraying-with-security-event-auditing)
