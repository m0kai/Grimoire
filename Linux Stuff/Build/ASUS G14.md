-- -
[ArchWiki Entry](https://wiki.archlinux.org/title/ASUS_Linux)
This is some drivers/software to add functionality for Asus laptops, some specifically for the G14. 
### Install via pacman
Add Sign keys to pacman
```bash
pacman-key --recv-keys 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
pacman-key --finger 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
pacman-key --lsign-key 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
pacman-key --finger 8F654886F17D497FEFE3DB448B15A6B0E9A3FA35
```
Add repo to pacman via config:
```bash
# in /etc/pacman.conf
[g14]
Server = https://arch.asus-linux.org
```
Update pacman:
```bash
sudo pacman -Syu
```
Install packages
```bash
# CUstom fan profiles, power profiles, animations, etc
sudo pacman -S asusctl power-profiles-daemon # install
sudo systemctl enable --now power-profiles-daemon.service # enable service

# graphics switching
sudo pacman -S supergfxctl switcheroo-control
sudo systemctl enable --now supergfxd
sudo systemctl enable --now switcheroo-control

# ROG Control Center
sudo pacman -S rog-control-center

# custom linux kernel, may not really be necessary
sudo pacman -Sy linux-g14 linux-g14-headers

# then if you use grub, otherwise you need to hunt for how to reconfig systemd or whatever. 
grub-mkconfig -o /boot/grub/grub.cfg
```

### Install via AUR
Did not work as well for me, and the docs say to do via pacman above
```bash
# If you do the pacman thing above, just do with pacman rather than yay
yay -S asusctl supergfxctl rog-control-center linux-g14 linux-g14-headers
```