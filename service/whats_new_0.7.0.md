# 0.7.0
- **Location tracking!** - I'm so excited to release this feature! Finally the `device_tracker` entity created by `mobile_app` integration will be updated with your current location! You can configure location tracking in "Integration settings" from main app menu. Have fun, but pay attention on changes made for this to work:
  - **Authentication** with Home Assistant login migrated from webview to deep links. Login form will be displayed now in a browser window.
  - **Webview panels** now will be opened in a Chrome custom tab (or browser window), so authenticated webviews will not work. It means that you'll need to login to your HA once again during first visit.
- **Tablet UI** - cards now distributed evenly by columns depending on screen width. Entity page for tablets and phones in landscape now will be shown as a panel in the right part of the screen.
![Tablet UI](http://ha-client.homemade.systems/assets/images/whats_new/0.7.0/tablet_ui_01.png)![Tablet UI with entity page](http://ha-client.homemade.systems/assets/images/whats_new/0.7.0/tablet_ui_02.png)
- **Independent service calls**. Now services will be called with http post request instead of waiton for socket connection. You can try to interact with entities even if there is "loading" indicator displayed.
- **Media players quick access**. The "TV" button in app header will now show the ammout of currently active media players (state `playing`, `paused` or `idle`). You can open media player page right from there to control it.
![Media players quick access](http://ha-client.homemade.systems/assets/images/whats_new/0.7.0/001.png)
- **Media player seek**. You can now set playing position with slider on player page for supported platforms.
![Media player seek](http://ha-client.homemade.systems/assets/images/whats_new/0.7.0/002.png)
- **Switch media player**. Going to another room? No problems, now you can switch currently playing media from one player to another.
- **Vacuum support**
- Entity history and attributes are now hidden by default on entity page and can be viewed expanding corresponding panel.
- "What's new" page
- Fix for missed group entities
- Gitpod environment configuration added
