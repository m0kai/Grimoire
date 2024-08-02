-- -
#### Install
At time of writing, install is done from AUR. This is likely to change given some time.
```bash
yay -S nordvpn-bin
```
#### Setup
```bash
# create group, should have been created during install
groupadd -r nordvpn

# add your user to the group
# need to restart for it to start working
sudo gpasswd -a <username> nordvpn

# enable and start NordVPN service
sudo systemctl enable --now nordvpnd.service
```
#### login using token
Log into [account](https://my.nordaccount.com) -> `services` -> `NordVPN` -> `Manual setup` -> `Set up NordVPN manually` -> `access token` then generate a token and copy it. Then:
```bash
nordvpn login --token "<access token>"
```
#### Connection management
```bash
# you can connect to a nearby server
nordvpn connect

# specify connection
nordvpn connect [[country]/[server]/[country_code]/[city] or [country] [city]]

# check status
nordvpn status

# disconnect 
nordvpn disconnect
```