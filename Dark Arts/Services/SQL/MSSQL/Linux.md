-- -
### CLI
```bash
sqsh -S <ip> -U <user> -P <passwd>
sqsh -S 10.129.20.13 -U username -P Password123
```
### GUI
Use [dbeaver](https://github.com/dbeaver/dbeaver). Download the release from [here](https://github.com/dbeaver/dbeaver/releases)
```bash
# assuming you are on a debian based system
sudo dpkg -i dbeaver-<version>.deb

# start the application 
dbeaver &

# then follow GUI instructions to get connected
```