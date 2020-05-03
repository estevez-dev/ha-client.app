# [Help pages](/help) - Mobile app integration

- [Device name](#device-name)
- [Notifications](#notifications)
- [Location tracking](#location-tracking)
- [Troubleshooting](#troubleshooting)

If this documentation was not useful enough for you, feel free to ask any question in [HA Client on Descord](https://discord.gg/nd6FZQ)

{% include in_post.html %}

Home Assistant [Mobile App Integration](https://www.home-assistant.io/integrations/mobile_app/) allows HA Client to handle push notifications and report your device location and battery state.

After successful login HA Client will automatically register itself on your Home Assistant to make notifications and location tracking possible and then will ask you to restart your server.

![image](/help/images/mobile_app_integration004.png)

You can find **Integration settings** in **App settings** from main HA Client menu.

![image](/help/images/mobile_app_integration001.png)

![image](/help/images/mobile_app_integration002.png)

![image](/help/images/mobile_app_integration003.png)

[Back to top](#help-pages---mobile-app-integration)

## Devcie name
On [first app start](/help/connection#quick-start) you can choose device name for your integration. All entity names created by this integration will depend on that name.

If you want to change device name for already created integration, you need to remove *Mobile App: [your device name]* from Home Assistant **Configuration** - **Integrations**, then restart your server and launch HA Client once again. The app will ask you to create new integration allowing to change default device name.

## Notifications

HA Client supports sending notifications from Home Assistant to the app.

For now notificationas could only have title and text. No actions supported yet. After mobile app will be registered and your Home Assistant will be restarted you'll get a new `notify` like `notify.mobile_app_egor_s_pixel_3_xl` (depends on [device name](#device-name)). It can be used to send notifications to HA Client on a specific device. Just call this service with some data:

```yaml
{"title":"Oi!", "message":"Something is moving on your backyard!"}
```

The `title` is not mandatory, by defauld it will be "HA Client".

[Back to top](#help-pages---mobile-app-integration)

## Location tracking

HA Client supports updating `device_tracker` entity with real device GPS location.

Location tracking is implemented with [Andorid Workmanager](https://developer.android.com/topic/libraries/architecture/workmanager). It means that background location tracking is battery friendly and work as intended from OS perspective.

After mobile app will be registered and your Home Assistant will be restarted you'll get a new `device_tracker` entity like `device_tracker.mobile_app_egor_s_pixel_3_xl` (depends on [device name](#device-name)). To start sending location to this entity you need to enable Location tracking in HA Client through **Integration settings** in **App settings**

![image](/help/images/mobile_app_integration001.png)

![image](/help/images/mobile_app_integration002.png)

![image](/help/images/mobile_app_integration006.png)

[Back to top](#help-pages---mobile-app-integration)

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
