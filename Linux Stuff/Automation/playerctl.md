-- -
Terminal control of audio playing on computer. If you don't specify the player, it will default to whatever the first one is, which isn't always useful.
```bash
# list currently available players
playerctl -l

# Toggle pause/play
playerctl play-pause

# specify a player
playerctl --player=[NAME] [command]
playerctl --player=spotify
playerctl --player=spoitfy play-pause

# check the status of the player
playerctl status # default player
playerctl --player=spotify status # specify player to check status
```

for testing:
```bash
# 02-05-2025
chromium.instance2979
```