# Documentation
## Table of content
- [Requirements](#requirements)
  - [Home Assistant general](#home-assistant-general)
  - [Port](#port)
  - [HTTP or HTTPS](#http-or-https)
  - [SSL Certificates](#ssl-certificates)
  - [Android](#android)
- [Authentication](#authentication)
- [UI configuration](#ui-configuration)
- [Log Viewer](#log-viewer)

## Requirements
### Home Assistant general
To check if you are using right configuration for app, try to access your Home Assistant web interface with the same protocol (http:// or https://), the same domain or IP and port. If it is not loading – the app will not work as well.

To connect to your Home Assistant instance with HA Client you need `http` and `websocket_api` components to be enabled as well as [remote access](https://www.home-assistant.io/docs/configuration/remote/) configured. If you are using `frontend` component (Home Assistant web interface actually) `websocket_api` is enabled by default and `http` component is already configured on your server, but still you need to double check.

In other cases changes should be made to you `configuration.yaml`:
```yaml
http:
  api_password: #some password here
  base_url: #your domain for Home Assistant instance
  ssl_certificate: /ssl/fullchain.pem #ssl configuration to access your HA by https
  ssl_key: /ssl/privkey.pem 

websocket_api:
```

[Back to top](#documentation)
### Port
By default your Home Assistant is using port number `8123`. But to access your instance from outside of your home network, probably you configured some port forwarding rules on you router. If you forward some other port from outside to `8123` port on Home Assistant IP, you need to use that port instead.

If you are accessing your web interface without port, then you need to try port `80` or `443` in app.

[Back to top](#documentation)
### HTTP or HTTPS
It is not required to use secure connection. Just remember: if you are accessing your web interface with http, you need to switch “Use ssl” off in app settings as well.

But if you are using ssl (accessing web interface with https://) – your certificate should be valid (not self-signed).

[Back to top](#documentation)
### SSL Certificates
The main requirement is that your SSL Certificate should not be self-signed. Most certificates from providers like Let’s Encrypt will work. There is [known issue](https://github.com/estevez-dev/ha_client_pub/issues/24) with RapidSSL certificate, but this problem is common not only for HA Client.

Using of self-signed certificate is not possible for now and this is a restriction of Flutter’s WebSocket implementation. To stay up to date with this issue solving or possible workarounds please [follow this issue in GitHub](https://github.com/estevez-dev/ha_client_pub/issues/3).

[Back to top](#documentation)
### Android
Minimum supported Android API level is 21. That’s Android 5.0 and higher.

[Back to top](#documentation)
## Authentication
Starting from Home Assistant 0.78.0 `api_password` is a deprecated way to authenticate third party apps and services. You should use long-lived access tokens instead. To make HA Client use access token to authenticate you need:
1. Go to your Home Assistant web interface and open your profile settings (just click on your user picture in the top part of left menu)

  ![image](/assets/images/ha_profile.png)
 
2. Scroll down to *Long-lived access tokens* section and click *Create token*

  ![image](/assets/images/ha_access_tokens.png)

3. Give it a name `HA Client` as it will be used only for HA Client app (it is recommended to use different access tokens for different apps and services)
4. Click *Ok* and copy newly generated access token somewhere in a safe place or directly to Connection settings of HA Client
  
  ![image](/assets/images/setting_access_token.png)

[Back to top](#documentation)
## UI Configuration
By default HA Client UI is based on your Lovelace UI config, so it should display the same views as your Home Assistant web UI. It is still possible to switch off Lovelace UI in app settings. In this case app UI will be based on groups configuration, the same as old Home Assistant UI.

  ![image](/assets/images/setting_ui.png)

[Back to top](#documentation)
## Log Viewer
There is a built in debug messages viewer in the app. You can access it by *Log* item in main menu. It will be very helpful if you will attach a copy of this log to your issue report. It is easy to do with button in header (![image](/assets/images/log_copy_btn.png)) that will copy all log entries to clipboard.

  ![image](/assets/images/log_viewer.png)

Please note that oldest entries goes first, so to see latest messages you need to scroll this view down.

[Back to top](#documentation)
