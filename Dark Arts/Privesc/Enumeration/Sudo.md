-- -
Look for shell escapes using sudo. Note, this usually requires you to have the password to the account you are currently on, but sometimes it does not, so always check!
```bash
sudo -l
```

^767678

Then type the programs output into [GTFOBins](https://gtfobins.github.io) and it should walk you through what you need to do. You may also be able to abuse custom software or custom scripts through this vector as well. 

More exploit information can be found [[Dark Arts/Privesc/Exploits/Sudo|here]]

#### LD_PRELOAD
You may find this when executing the above command. When you do, before it lists the software that can be used with sudo privs, you will see the following line:
`env_reset, env_keep+=LD_PRELOAD`
This may suggest a complex privesc attack vector, if you see this check out the [[LD_PRELOAD]] exploit page ^866a8f