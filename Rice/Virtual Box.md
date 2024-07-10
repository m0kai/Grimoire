-- -
Various tricks I've learned to get Virtual Box working on Arch w/ full screen support and what not.
## Install
#### Arch
[source](https://wiki.archlinux.org/title/VirtualBox )
Doubt you'll need the steps anywhere else nor do I think you will use any other distro:
```bash
# if you install: virtualbox-guest-iso
# then you can probably skip the Guest additions section below. I'm just illiterate so I didn't read far enough down the page to see it was a separate package in pacman.
sudo pacman -S virtualbox virtualbox-guest-iso
```
It'll ask you which package to choose:
```bash
# note: this is the option for the "linux" kernel, for anything else pick the other option.
virtualbox-host-modules-arch
```
## Turn off Mini Toolbar
This is required when using a window manager rather than a desktop environment. Required for #hyprland but I saw in the forums that it was required for #i3wm as well, so seems like its a problem with any window manage on any compositor bc Oracle had to be a special snowflake. 
On the main menu, click on your VM:
`Settings` -> `User Interface` -> `Mini Toolbar` -> Deselect:  `Show in Full-screen/Seamless`
*Note: the VM's OS also does not matter, I had to do this on a Windows VM to get it to work as well *
## Guest Additions
Mostly to get full screen working. Required for Hyprland, but it's likely required for any WM/Desktop environment on arch.
#### Kali Linux VM
[Source](https://www.kali.org/docs/virtualization/install-virtualbox-guest-additions/)
**In the VM:**
```bash
sudo apt update
sudo apt upgrade
sudo apt install -y --reinstall virtualbox-guest-x11
sudo reboot -f
```