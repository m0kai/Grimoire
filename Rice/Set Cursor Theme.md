-- -
This one is imperfect because I'm not sure how exactly I got it working, so I am documenting what *seemed* to work here and on subsequent builds, I'll figure out how exactly I got it working and try to automate it. TLDR; It's a future Cris problem
```bash
# Download the theme from gnome looks
# install nwg-look
sudo pacman -S nwg-look

# run it
nwg-look

# Go to settings for cursor and set the theme there. Click apply.
# try restarting hyprland w/ SUPER+M
# See if it actually applied it.

# otherwise, use hyprctl
# note that the size is by default 24
hyprctl setcursor [THEME] [SIZE]

# Then restart hyprland w/ SUPER+M
```