-- -
Randomly, when I tried using my razer wireless mouse on my second monitor via HDMI, the cursor would start lagging/framerate drop. Lots of things I tried, but it ended up being a config fix:
```bash
# inside you hyprland.conf
cursor {
	no_hardware_cursors = true
}
```