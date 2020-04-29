# [Help pages](/help) - Connection
If this documentation was not useful enough for you, feel free to ask any question in [HA Client on Descord](https://discord.gg/nd6FZQ)

- [Quick start](#quick-start)
- [Advanced](#advanced)
  - [Port](#port)
  - [HTTP or HTTPS](#http-or-https)
  - [SSL Certificates](#ssl-certificates)
  - [Login with long-lived token](#login-with-long-lived-token)

## Quick start
The quick and easy whay to connect HA Client with your Home Assistant server is to use [Remote UI](https://www.nabucasa.com/config/remote/). If you alredy had it set up, just open your Home Assistant UI in browser, go to **Configuration** - **Home Assistant Cloud**, find **Remote Control** section and copy the url from **Your instance is available at**.

![image](/help/images/connection001.png)

![image](/help/images/connection002.png)

Then just go to **App settings** in HA Client, choose **Connection settings**, put copied url to **Home Assistant url** field ignoring all other fields and hit **Apply**.

![image](/help/images/connection003.png)

![image](/help/images/connection004.png)

![image](/help/images/connection005.png)

Now you need to login. And this process will be almost automatic thanks to [Home Assistant Authentication API](https://developers.home-assistant.io/docs/en/auth_api.html). You'll see a login form loaded directly from your Home Assistant instance:

![image](/help/images/connection006.png)

That's it! You are ready to go.

[Back to top](#help-pages---connection)

## Advanced
### Port
You don't need to worry about port if you are using [Remote UI](https://www.nabucasa.com/config/remote/). Just leave it blank.

By default your Home Assistant is using port number `8123`. But to access your instance from outside of your home network, probably you configured some port forwarding rules on you router. If you forward some other port from outside to `8123` port on Home Assistant IP, you need to use that port instead.

If you are accessing your web interface without port, then you need to try port `80` or `443` in app.

You can also try to leave port number field blank to make HA Client to try to choose port for you. May be it will succeed.

[Back to top](#help-pages---connection)
### HTTP or HTTPS
You don't need to worry about this option if you are using [Remote UI](https://www.nabucasa.com/config/remote/). Just leave it as is.

It is not required to use secure connection. Just remember: if you are accessing your web interface with `http`, you need to switch “Use ssl” off in app settings as well.

But if you are using ssl (accessing web interface with `https://`) – your certificate should be valid and **not self-signed**. This is not a restriction of HA Client, but a known issue of Flutter framework.

[Back to top](#help-pages---connection)
### SSL Certificates
The main requirement is that your SSL Certificate should not be self-signed. Most certificates from providers like Let’s Encrypt will work. There is [known issue](https://github.com/estevez-dev/ha_client_pub/issues/24) with RapidSSL certificate, but this problem is common not only for HA Client.

Using of self-signed certificate is not possible for now and this is a restriction of Flutter’s WebSocket implementation.

[Back to top](#help-pages---connection)

### Login with long-lived token
It is possible to generate long-lived token manually and set the app to use it instead of logging in with a simple OAuth way.
To make HA Client use your generated long-lived token you need:
1. Go to your Home Assistant web interface and open your profile settings (just click on your user picture in the bottom part of main menu)

  ![image](/help/images/connection007.png)
 
2. Scroll down to **Long-lived access tokens** section and click **Create token**

  ![image](/help/images/connection008.png)

3. Give it a name `HA Client` as it will be used only for HA Client app (it is recommended to use different access tokens for different apps and services)
4. Click **Ok** and copy newly generated access token somewhere in a safe place or directly to **Connection settings** of HA Client and hit **Apply**
  
  ![image](/help/images/connection009.png)

[Back to top](#help-pages---connection)



### [What you need](/help/what_you_need) < Previous | Next > [User Interface](/help/user_interface)
