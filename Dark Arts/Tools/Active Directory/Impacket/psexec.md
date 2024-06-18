-- -
A clone of the sysinternals psexec that works slightly differently. It creates a remote service using a randomly named executable that is uploaded to the `ADMIN$` share on a target host. It registers the service via `RPC` and the `Windows Service Control Manager`. Communication then proceeds over a named pip and it gives you a remote `SYSTEM` shell.
#### Basic Usage (auth)
```bash
psexec.py <domain>/<user>:'<passwd>'@<target ip>
psexec.py inlanefreight.local/wley:'transporter@4'@172.16.5.125
```

^d07ccd
