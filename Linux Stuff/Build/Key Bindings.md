-- -
Most of this will be for hyprland, which I haven't added notes for yet.
### Custom "non-standard" keybindings
Most key bindings for a computer are standard across the board, but for the function keys or special "M" keys (ASUS G14 laptop), you may want to find out it's code so you can bind stuff to it. 
```bash
# to find out a usable code for your key, use wev
# install:
sudo pacman -S wev

# then just run:
wev

# this will open a white checkered window, within that window, hit whatever key you are looking for, it will spit out various values, but you are interested in the value:
# key: 78
# that number tells you what code to put into the hyprland config:
# bind =,code: 78, exec, <cmd>

# this will create the binding to whatever key corresponds to 78
```