-- -
Look for shell escapes using sudo. Note, this usually requires you to have the password to the account you are currently on, but 'ometimes it does not, so always check!
```bash
sudo -l
```

^767678

Then type the programs output into [GTFOBins](https://gtfobins.github.io) and it should walk you through what you need to do. You may also be able to abuse custom software or custom scripts through this vector as well. 

More exploit information can be found [[Dark Arts/Privesc/Linux/Exploits/Sudo/~Home|here]]

#### LD_PRELOAD
You may find this when executing the above command. When you do, before it lists the software that can be used with sudo privs, you will see the following line:
`env_reset, env_keep+=LD_PRELOAD`
This may suggest a complex privesc attack vector, if you see this check out the [[LD_PRELOAD]] exploit page ^866a8f

#### CVE-2019-18634
#cve-2019-18634
Buffer overflow vulnerability in sudo. Key component is the version of sudo and that the `pwfeedback` setting is on. 
##### Enum
```bash
# get config info, may not work
sudo -l
cat /etc/sudoers

# if config doesn't work, then you can sudo something and when it asks for the password, you type some random shit in. If you see the asterisks, then the pwfeedback setting is on!

# Get sudo version
# looking for any version previous to 1.8.26
sudo -V
```

^297150

From here, [[CVE Exploits#^8d0e58|exploit]]