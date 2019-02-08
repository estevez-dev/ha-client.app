# Table of content
- [Requirements](#requirements)
  - [Home Assistant general](#home-assistant-general)
  - Port
  - HTTP or HTTPS
  - SSL Certificates
  - Android
- Authentication
- UI configuration
  - Lovelace UI
- Log Viewer

# Requirements
## Home Assistant general
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
