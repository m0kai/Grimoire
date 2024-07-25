-- -
Drops a semi-interactive shell through the `Windows Management Instrumentation`. Commands will be run as a local admin user which may be stealthier than methods such as psexec, but will still likely be caught by AV and EDR systems. Will also not produce a file artifact such as psexec.
#### Basic Usage (auth)
```bash
wmiexec.py <domain>/<user>:'<passwd>'@<target ip>
wmiexec.py inlanefreight.local/wley:'transporter@4'@172.16.5.5  
```

^2a6f1f
