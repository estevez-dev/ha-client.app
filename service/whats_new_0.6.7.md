# 0.6.7
- **Tablet UI** - cards now distributed evenly by columns depending on screen width. Entity page for tablets and phones in landscape now will be shown as a panel in the right part of the screen.
- **Independent service calls**. Now services will be called with http post request instead of waiton for socket connection. You can try to interact with entities even if there is "loading" indicator displayed.
- **Media players quick access**. The "TV" button in app header will now show the ammout of currently active media players (state `playing`, `paused` or `idle`). You can open media player page right from there to control it.
- **Media player seek**. You can now set playing position with slider on player page for supported platforms.
- **Switch media player**. Going to another room? No problems, now you can switch currently playing media from one player to another.
- Entity history and attributes are now hidden by default on entity page and can be viewed expanding corresponding panel.
- "What's new" page
# 0.6.6
- **Share media url to any media_player!** You can now use Android share menu to share any url to HA Client. HA Client will ask you to choose one of your media players and try to play that media on selected player. Media extractor also supported.
- **Gauge card** support
- **Lovelace view as panel** support
- **Glance card improvements**. It will now fit as many icons as you set in config.
- Conditional card fix
- Camera stream now will be launched in Chrome Custom Tab, not in webview to fix initial scale issues.
- Button-entity card improvements. It's just looks better now.
