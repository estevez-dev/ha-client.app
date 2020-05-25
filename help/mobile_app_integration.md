# [Help pages](/help) - Mobile app integration

- [Device name](#device-name)
- [Notifications](#notifications)
- [Location tracking](#location-tracking)
- [Troubleshooting](#troubleshooting)

If this documentation was not useful enough for you, feel free to ask any question in [HA Client on Descord](https://discord.gg/u9vq7QE)

{% include in_post.html %}

Home Assistant [Mobile App Integration](https://www.home-assistant.io/integrations/mobile_app/) allows HA Client to handle push notifications and report your device location and battery state.

After successful login HA Client will automatically register itself on your Home Assistant to make notifications and location tracking possible and then will ask you to restart your server.

![image](/help/images/mobile_app_integration004.png)

You can find **Integration settings** in **App settings** from main HA Client menu.

![image](/help/images/mobile_app_integration001.png)

![image](/help/images/mobile_app_integration002.png)

![image](/help/images/mobile_app_integration003.png)

[Back to top](#help-pages---mobile-app-integration)

## Device name
On [first app start](/help/connection#quick-start) you can choose device name for your integration. All entity names created by this integration will depend on that name.

If you want to change device name for already created integration, you need to remove *Mobile App: [your device name]* from Home Assistant **Configuration** - **Integrations**, then restart your server and launch HA Client once again. The app will ask you to create new integration allowing to change default device name.

## Notifications

HA Client supports sending notifications with custom actions from Home Assistant to the app. Actions could trigger events of call services.

After mobile app will be registered and your Home Assistant will be restarted you'll get a new `notify` like `notify.mobile_app_egor_s_pixel_3_xl` (depends on [device name](#device-name)). It can be used to send notifications to HA Client on a specific device. Just call this service with data:

```yaml
title: "Oi!"
message: "Something is moving on your backyard!"
data:
  tag: camera_movement
  image: http://myserver.co.uk/cameraImage.jpeg
  autoDismiss: false
  actions:
    - action: call-service
      title: "Service action"
      service: light.turn_on
      service_data:
        entity_id: light.living_room
    - action: my_action
      title: "Event action"
```
#### options for **notify** service data

| Option | Value | Description |
| ------------- | ------------- | ----- |
| title  | *String* | Notification title. Default is `HA Client` |
| message | *String*  | Notification body |
| data | *Object*  | Notification settings |

#### options for **data**

| Option | Value | Description |
| ------------- | ------------- | ----- |
| tag  | *String* | Notification tag. Not mandatory. Use it to replace existing notification with the same tag |
| image | *String*  | Image url to be shown in notification |
| dismiss | `true` or `false` | Use it to dismiss excisting notification with specific `tag`. Default is `false` |
| autoDismiss |  `true` or `false` | If `false` notification will not be dismissed after click/tap on its body or action. Default is `true` |
| channelId | *String*  | Custom notification channel to create and use. Default is `ha_notify` |
| actions | *List*  | Up to 3 actions to add to the notification |

#### options for **actions** item

| Option | Value | Description |
| ------------- | ------------- | ----- |
| action | `call-service` or  *String* | Will try to call service or fire an event to your Home Assistant. Event type will be `ha_client_event` and `action` value will be passed in `data` of event |
| title | *String*  | Button title for action |
| service | *String* | Home Assistant service to be called if `action` is `call-service` |
| service_data |  *Object* | Any set of data to be passed to `service`. For example: `entity_id` |

[Back to top](#help-pages---mobile-app-integration)

{% include in_post.html %}

## Location tracking

HA Client supports updating `device_tracker` entity with real device GPS location.

Location tracking is implemented with [Andorid Workmanager](https://developer.android.com/topic/libraries/architecture/workmanager). It means that background location tracking is battery friendly and work as intended from OS perspective.

After mobile app will be registered and your Home Assistant will be restarted you'll get a new `device_tracker` entity like `device_tracker.mobile_app_egor_s_pixel_3_xl` (depends on [device name](#device-name)). To start sending location to this entity you need to enable Location tracking in HA Client through **Integration settings** in **App settings**

![image](/help/images/mobile_app_integration001.png)

![image](/help/images/mobile_app_integration002.png)

![image](/help/images/mobile_app_integration006.png)

[Back to top](#help-pages---mobile-app-integration)

{% include in_post.html %}

## Troubleshooting
If notifications or location tracking doesn't work, first thing you need to check is entities name you are using. You can check that in **Configuration** - **Integrations** - **Mobile App: [your device name]** in your Home Assistant.

Also it could be useful to remove Mobile App integration from Home Assistant and restrat server to allow HA Client to create integration once again.

### Notification issues
There is a restriction on daily notifications count for each device: **50**.

### Location tracking issues
- Make sure the Location permission is granted for HA Client.
- You can disable background location tracking task and enable it again to resolve possible issues. Go to _Integration settings_ in HA Client and disable Location tracking to cancel backgroud tasks. Then enable it back.
- You can add exception for HA Client in battery saving settings on your Android device to improve background tasks execution. This can help solving some location tracking issues on older Android versions. It can be achieved differently on different Android versions and even on different devices. For example in Android 10 on Pixel phones you need to go to _Settings_ -> _Apps & notifications_ tap _Advanced_ -> _Special app access_ -> _Battery optimization_. Or simply search for _Battery optimization_ on main _Settings_ screen with search field. Inside _Battery optimization_ switch to _All apps_, find _HA Client_ in the list and tap it. On the popup appeared choose _Don't optimize_:

![Battery optimization](/help/images/mobile_app_integration005.png)

[Back to top](#help-pages---mobile-app-integration)

### [User interface](/help/user_interface) < Previous | Next > [Additional features](/help/additional_features)
