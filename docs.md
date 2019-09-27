# Documentation
## Table of content
- [Requirements](#requirements)
  - [Home Assistant general](#home-assistant-general)
  - [Port](#port)
  - [HTTP or HTTPS](#http-or-https)
  - [SSL Certificates](#ssl-certificates)
  - [Android](#android)
- [Authentication](#authentication)
- [Mobile app integration](#mobile-app-integration)
  - [Notifications](#notifications)
- [UI configuration](#ui-configuration)
- [Log Viewer](#log-viewer)

## Requirements
### Home Assistant general
To check if you are using right configuration for app, try to access your Home Assistant web interface with the same protocol (http:// or https://), the same domain or IP and port. If it is not loading – the app will not work as well.

To connect to your Home Assistant instance with HA Client you need `mobile_app` component to be enabled. Just add (or check if exist) this line to your `configuration.yaml`:

```yaml
mobile_app:
```

Also to make HA Client work outside of your home network [remote access](https://www.home-assistant.io/docs/configuration/remote/) should be configured or [Remote UI](https://www.nabucasa.com/config/remote/) should be used.

[Back to top](#documentation)
### Port
By default your Home Assistant is using port number `8123`. But to access your instance from outside of your home network, probably you configured some port forwarding rules on you router. If you forward some other port from outside to `8123` port on Home Assistant IP, you need to use that port instead.

If you are accessing your web interface without port, then you need to try port `80` or `443` in app.

[Back to top](#documentation)
### HTTP or HTTPS
It is not required to use secure connection. Just remember: if you are accessing your web interface with `http`, you need to switch “Use ssl” off in app settings as well.

But if you are using ssl (accessing web interface with `https://`) – your certificate should be valid (not self-signed). This is not a restriction of HA Client, but a known issue of Flutter framework.

[Back to top](#documentation)
### SSL Certificates
The main requirement is that your SSL Certificate should not be self-signed. Most certificates from providers like Let’s Encrypt will work. There is [known issue](https://github.com/estevez-dev/ha_client_pub/issues/24) with RapidSSL certificate, but this problem is common not only for HA Client.

Using of self-signed certificate is not possible for now and this is a restriction of Flutter’s WebSocket implementation. To stay up to date with this issue solving or possible workarounds please [follow this issue in GitHub](https://github.com/estevez-dev/ha_client_pub/issues/3).

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
  
For now it means that you can use [notofications](#notifications) in HA Client. But to make new `notify` service appear you need to restart Home Assistant.

[Back to top](#documentation)
### Notifications
**(HA Client >= 0.6.0)**
Starting from version 0.6.0 HA Client supports sending notifications from Home Assistant to the app. The app [should be registered in your HA](#mobile-app-integration) and HA need to be restarted to make it work.

For now notificationas could only have title and text. No actions supported yet. After [mobile app will be registered](#mobile-app-integration) and your Home Assistant will be restarted you'll see a new `notify` service. For example: `notify.mobile_app_egor_s_pixel_3_xl`. It can be used to send notifications to HA Client on a specific device. Just call this service with some data:
```yaml
{"title":"Oi!", "message":"Something is moving on your backyard!"}
```
The `title` is not mandatory, by defauld it will be "HA Client".
#### Important!
For now Home Assistant don't have a way to detect was current application on current device already registered or not. That is why if you will reinstall HA Client or clear all app data, the app will be registered once again and another Integration will be created on your Home Assistant:

  ![image](/assets/images/duplicate_integration.png)
  
As well as second `notify` service and second `device_tracker` entity. **Notifications will not be handled by HA Client**. To fix this you need to got to *Configuration* - *Integrations* in your Home Assistant and remove any Integration created by HA Client for your device. Then you need to restart Home Assistant server to make all exces entities to be removed.

After that you can go to *Config* in HA Client, scroll down to *Mobile app* and *Reset registration*. A new Integration will be created and Home Assistant server should be restarted once again. Notifications should be handled properly now. 

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
