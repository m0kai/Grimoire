-- -
This is for getting browsers to play nice with wayland. At least at time of writing. A couple of notes to keep in mind:
1. This was found under help getting NVIDIA drivers to work with the browser, may be different for other GPU manufacturers, or may not.
2. The settings page says `chrome` so I am assuming it only works on Chromium based browsers, and would be different for anything else. Seems to have fixed `Opera` and `Vivaldi`, which are proprietary but I believe they are both Chromium/Chrome based. 
#### My Steps
1. Open Browser
2. Enter `chrome://flags`
3. In the search bar, type: `wayland`
4. Change Ozone setting from `Default` to `Wayland`
5. Apply setting which should restart the browser for you.
#### Forum Steps
https://github.com/Alex313031/thorium/issues/446
1. Open browser
2. Enter `chrome://flags`
3. In the search bar, type: `wayland`
4. Enable WebRTC PipeWire support and Preferred Ozone platform if they aren't.
5. Restart Browser
