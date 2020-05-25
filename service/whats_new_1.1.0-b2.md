## 1.1.0-beta2
- **Actionable notifications**. Actions could call service or fire events. The event type is `ha_client_event`.
- **Images in notifications**. Just add `image` to the notification `data`.
## 1.1.0-beta
- **Full badges support** including *entity_filter*
- **Light card suppot**. Brightness could be changed by tapping, but not dragging for now. Dragging support will be added later
- **States-like UI** are now generated if you don't have Lovlease UI config yet
- **Quick access buttons** moved to the center of app header. New button for lights added allowing to turn on or off all lights
- Lables for Light controll sliders
- Getting Lovelace UI config now works fine with HA < 0.107
- Fix for panel view
- Custom cards are now hidden
- Cards with errors are now hidden
- Cards display improvements
- Entity icons display improvements
- Fix of empty stack cards issue
- Improve HA OAuth login for old devices
- Unneeded external bus support disabled for authenticated webview
- Bug fixes
