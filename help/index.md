# HA Client help pages
If this documentation was not useful enough for you, feel free to ask any question in [HA Client on Descord](https://discord.gg/nd6FZQ)
## Table of content
- [What you need](/help/what_you_need)
  - [Home Assistant](/help/what_you_need#home-assistant)
  - [Android](/help/what_you_need#android)




- [Authentication](#authentication)
- [Mobile app integration](#mobile-app-integration)
  - [Notifications](#notifications)
  - [Location tracking](#location-tracking)
  - [Integration troubleshooting](#integration-troubleshooting)
- [UI configuration](#ui-configuration)
- [Log Viewer](#log-viewer)

## Requirements
### Home Assistant general
#### Requires Home Assistant 0.104 or higher!
To check if you are using right configuration for app, try to access your Home Assistant web interface with the same protocol (http:// or https://), the same domain or IP and port. If it is not loading – the app will not work as well.

To connect to your Home Assistant instance with HA Client you need `mobile_app` component to be enabled. If you have `default_config` in your `configuration.yaml` you don't need to add anything. If not - just add (or check if exist) this line to your `configuration.yaml`:

```yaml
mobile_app:
```

Also to make HA Client work outside of your home network [remote access](https://www.home-assistant.io/docs/configuration/remote/) should be configured or [Remote UI](https://www.nabucasa.com/config/remote/) should be used.

[Back to top](#documentation)
### Port
You don't need to worry about port if you are using [Remote UI](https://www.nabucasa.com/config/remote/). Just leave it blank.

By default your Home Assistant is using port number `8123`. But to access your instance from outside of your home network, probably you configured some port forwarding rules on you router. If you forward some other port from outside to `8123` port on Home Assistant IP, you need to use that port instead.

If you are accessing your web interface without port, then you need to try port `80` or `443` in app.

You can also try to leave port number field blank to make HA Client to try to choose port for you. May be it will succeed.

[Back to top](#documentation)
### HTTP or HTTPS
You don't need to worry about this option if you are using [Remote UI](https://www.nabucasa.com/config/remote/). Just leave it as is.

It is not required to use secure connection. Just remember: if you are accessing your web interface with `http`, you need to switch “Use ssl” off in app settings as well.

But if you are using ssl (accessing web interface with `https://`) – your certificate should be valid and **not self-signed**. This is not a restriction of HA Client, but a known issue of Flutter framework.

[Back to top](#documentation)
### SSL Certificates
The main requirement is that your SSL Certificate should not be self-signed. Most certificates from providers like Let’s Encrypt will work. There is [known issue](https://github.com/estevez-dev/ha_client_pub/issues/24) with RapidSSL certificate, but this problem is common not only for HA Client.

Using of self-signed certificate is not possible for now and this is a restriction of Flutter’s WebSocket implementation.

[Back to top](#documentation)
### Android
Minimum supported Android API level is 21. That’s Android 5.0 and higher.

[Back to top](#documentation)
## Authentication
{% include in_post.html %}
There is two ways to login to Home Assistant with HA Client
### Home Assistant OAuth
HA Client will login through [Home Assistant Authentication API](https://developers.home-assistant.io/docs/en/auth_api.html). You don't need to create and recreate access tokens. If HA Client is not authenticated yet or there is some issues logging in, it will ask you to login to your Home Assistant web interface with your credentials:

![image](/assets/images/oauth.png)

After successfull login HA Client will get secure code, request long-lived token from Home Assistant automatically and store it in secure storage of your Android device.

There is also 'Logout' option added. It will disconnect from Home Assistant, clear the UI and remove long-lived token from secure storage:

![image](/assets/images/logout.png)

[Back to top](#documentation)
### Manual long-lived token
It is possible to generate long-lived token manually and set the app to use it instead of logging in with a simple OAuth way.
To make HA Client use your generated long-lived token you need:
1. Go to your Home Assistant web interface and open your profile settings (just click on your user picture in the top part of left menu)

  ![image](/assets/images/ha_profile.png)
 
2. Scroll down to *Long-lived access tokens* section and click *Create token*

  ![image](/assets/images/ha_access_tokens.png)

3. Give it a name `HA Client` as it will be used only for HA Client app (it is recommended to use different access tokens for different apps and services)
4. Click *Ok* and copy newly generated access token somewhere in a safe place or directly to Connection settings of HA Client
  
  ![image](/assets/images/setting_access_token.png)

[Back to top](#documentation)
## Mobile app integration
{% include in_post.html %}
**(HA Client >= 0.6.0)**
Strating from 0.6.0 `mobile_app` component should be enabled on your Home Assistant server. If it is disabled, the app will show you an error saying that you need to enable `mobile_app` component on your HA instance. In that case just add this to your `configuration.yaml`:

```yaml
mobile_app:
```

If `mobile_app` component is enabled, you'll see a message about successfull mobile app registration:

  ![image](/assets/images/mobile_app_registered.png)
  
Also new integration will be created in your Home Assistant Integrations:

  ![image](/assets/images/mobile_app_registered-2.png)
  
It means that you can use [notifications](#notifications) and [location tracking](#location-tracking) in HA Client. But to make new `notify` service appear you need to restart Home Assistant.

**(HA Client >= 0.7.0)** _Integration settings_ item is available in main menu for mobile app integration configuration:

![Integration settings](/assets/images/103239-01.jpeg)

[Back to top](#documentation)
### Notifications
**(HA Client >= 0.6.0)**
Starting from version 0.6.0 HA Client supports sending notifications from Home Assistant to the app. The app [should be registered in your HA](#mobile-app-integration) and HA need to be restarted to make it work.

For now notificationas could only have title and text. No actions supported yet. After [mobile app will be registered](#mobile-app-integration) and your Home Assistant will be restarted you'll see a new `notify` service. For example: `notify.mobile_app_egor_s_pixel_3_xl`. It can be used to send notifications to HA Client on a specific device. Just call this service with some data:
```yaml
{"title":"Oi!", "message":"Something is moving on your backyard!"}
```
The `title` is not mandatory, by defauld it will be "HA Client".

Please note: there is a restriction on daily notifications count for each device: **150**. 
### Location tracking
**(HA Client >= 0.7.0)**
Starting from version 0.7.0 HA Client supports updating `device_tracker` entity with real device GPS location. The app [should be registered in your HA](#mobile-app-integration) and HA need to be restarted to make it work.

Location tracking is implemented with [Andorid Workmanager](https://developer.android.com/topic/libraries/architecture/workmanager). It means that background location tracking is battery friendly and work as intended from OS perspective. But it also means that:

#### If you want your location to be updated with exact the same intervhals you set in HA Client
you need to add exaption for HA Client in battery saving settings on your Android device. It can be achieved differently on different Android versions and even on different devices. For example in Android 10 on Pixel phones you need to go to _Settings_ -> _Apps & notifications_ tap _Advanced_ -> _Special app access_ -> _Battery optimization_. Or simply search for _Battery optimization_ on main _Settings_ screen with search field. Inside _Battery optimization_ switch to _All apps_, find _HA Client_ in the list and tap it. On the popup appeared choose _Don't optimize_:

![Battery optimization](/assets/images/114551.png)

After [mobile app will be registered](#mobile-app-integration) and your Home Assistant will be restarted you'll see a new `device_tracker` entity. For example: `device_tracker.mobile_app_egor_s_pixel_3_xl`. To start sending location to this entity you need to enable Location tracking in HA Client through _Integration settings_ item in main menu (HA Client >= 0.7.0):

![Location tracking settings](/assets/images/103202.png)

### Integration troubleshooting
#### Notification issues
Please note: there is a restriction on daily notifications count for each device: **150**.

For now Home Assistant don't have a way to detect was current application on current device already registered or not. That is why if you will reinstall HA Client or clear all app data, the app will be registered once again and another Integration will be created on your Home Assistant:

  ![image](/assets/images/duplicate_integration.png)
  
As well as second `notify` service and second `device_tracker` entity. **Notifications will not be handled by HA Client**. To fix this you need to got to *Configuration* - *Integrations* in your Home Assistant and remove any Integration created by HA Client for your device. Then you need to restart Home Assistant server to make all exces entities to be removed.

Then just open HA Client app. It will check mobile app integration and ask you to registrer a new one.
#### Location tracking issues
- If the [issue with duplicate integration](#notification-issues) is not your case but your `device_tracker` location is not updating as intended, please check [location tracking section](#if-you-want-your-location-to-be-updated-with-exact-the-same-intervhals-you-set-in-ha-client) of this guide.
- Also make sure the Location permission is granted for HA Client.
- You can disable background location tracking task and enable it again to resolve possible issues. Go to _Integration settings_ from HA Client main menu and disable Location tracking to cancel backgroud tasks. Then enable it back. 

[Back to top](#documentation)
## UI Configuration
{% include in_post.html %}
By default HA Client UI is based on your Lovelace UI config, so it should display the same views as your Home Assistant web UI. It is still possible to switch off Lovelace UI in app settings. In this case app UI will be based on groups configuration, the same as old Home Assistant UI.

  ![image](/assets/images/setting_ui.png)

[Back to top](#documentation)
## Log Viewer
There is a built in debug messages viewer in the app. You can access it by *Log* item in main menu. It will be very helpful if you will attach a copy of this log to your issue report. It is easy to do with button in header (![image](/assets/images/log_copy_btn.png)) that will copy all log entries to clipboard.

  ![image](/assets/images/log_viewer.png)

Please note that oldest entries goes first, so to see latest messages you need to scroll this view down.

[Back to top](#documentation)

If this documentation was not useful enough for you, feel free to ask any question in [HA Client community on Spectrum.chat](https://spectrum.chat/ha-client)
