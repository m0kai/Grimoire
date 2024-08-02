-- -
### Description
At the time of writing, it is not plug-and-play to get nvidia gpus (or maybe just the 3070 Mobile on the alienware laptop) working with wayland. To be more specific, if I use open source drivers, wayland does work but those drivers don't seem to work well for hashcat nor gaming. When installing the proprietary drivers, wayland needs some further configurations to get it to work so I can use hyprland, hashcat, and game. The following outlines what I did with my alienware m15 R4 laptop to get it to work properly.
### Reference
- https://www.maketecheasier.com/wayland-work-with-nvidia-graphics-cards/
### Steps
#### Setup environment
Environment config file location: `/etc/environment`
Backup just in case: `sudo cp /etc/environment ~/environment.bak`

*Note: Realistically, this file will probably be empty except for comments so the backup isn't really necessary*

**Add the following to the file**
```bash
QT_QPA_PLATFORMTHEME="wayland;xcb"
GBM_BACKEND=nvidia-drm
__GLX_VENDOR_LIBRARY_NAME=nvidia
ENABLE_VKBASALT=1
LIBVA_DRIVER_NAME=nvidia
WLR_NO_HARDWARE_CURSORS=1 # may not be necessary, for if the cursor isn't visible
```

#### Build init Ramdisk
*Note: this seems to only be for Arch builds*
Config Location: `/etc/mkinitcpio.conf`
**Add to the modules set**
```bash
MODULES=(nvidia nvidia_modeset nvidia_uvm nvidia_drm)
```
*Note: nothing should be in the modules set, but if there is something in there, just add the nvidia value in addition to whatever is in there.*

Then regenerate your initial ramdisk:
`sudo mkinitcpio -P`
##### Enable Direct Rendering Manager
Allows the kernel to work with GPUs. For Nvidia and Wayland to get along, we need to enable this. This is done by the bootloader, so depending on which one you are using, the steps will be slightly different. I will outline how to do it in GRUB and systemd. Of note, what has worked for me is the systemd steps, GRUB is untested but since it's the same shit different font, it should work the same way. 
**systemd**
Config location: `boot/loader/entries/2024-06-17_18-01-06_linux.conf`
*Note: the file is specified in the Arch Docs as loader.conf, but in practice there are two files in here one has the date and time of creation then _linux.conf and the other is a fallback, edit whichever ends with "_linux.conf"*
**Add to the end of the config**
```
nvidia-drm.modeset=1
```
**Reference**
[archwiki entry](https://wiki.archlinux.org/title/Systemd-boot)
Under 4.1 Loader configuration

**GRUB**
Edit `/etc/default/grub`
```
GRUB_CMDLINE_LINUX_DEFAULT="nvidia-drm.modeset=1"
```
Update GRUB configuration: `sudo grub-mkconfig -o /boot/grub/grub.cfg`
#### End
After the above steps, reboot and everything should be good to go. 
#### Post activities
```bash
# To get Hashcat working, install CUDA toolkit
sudo pacman -S cuda

# To start gaming just install steam
# make sure to enable steamplay or whatever in the settings after isntall
sudo pacman -S steam
```