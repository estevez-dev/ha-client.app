- **Actionable notifications**. Actions could call service or fire events. The event type is `ha_client_event`.
- **Additional notification options**. Add `image` to the notification `data` with image url to show image in notification. Use `tag` in notification `data` to replace already exsisting notification with the same `tag`. Use `dismiss: true` in notification `data` to dismiss previously shown notification with the same `tag`. Use `autoDismiss: false` to prevent notification from being dismissed after tap/click. Use `channelId` to create and use custom notification channels.
### Example of `notify` service data:
```
message: "Notification text"
title: "Hey!"
data:
  tag: myNotificationTag
  autoDismiss: false
  actions:
    - action: call-service
      title: Call service
      service: light.turn_on
      service_data:
        entity_id: light.hallway
    - action: my_event_action
      title: Fire event
```
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
