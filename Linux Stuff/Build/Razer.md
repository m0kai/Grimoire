-- -
[ArchWiki Entry](https://wiki.archlinux.org/title/Razer_peripherals)
Can customize **some** razer products:
```bash
sudo pacman -S openrazer-daemon

# make sure to add your user to group
sudo gpasswd -a $USER plugdev

# install front end
yay -S razercommander-git
```