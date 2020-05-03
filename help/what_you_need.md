# [Help pages](/help) - What You Need

- [Home Assistant](#home-assistant)
- [Android](#android)

{% include in_post.html %}

If this documentation was not useful enough for you, feel free to ask any question in [HA Client on Descord](https://discord.gg/u9vq7QE)

## Home Assistant
Of course you need [Home Assistant](https://www.home-assistant.io/) to make HA Client work. The version of Home Assintant should be **0.104** or higher.

To connect to your Home Assistant instance with HA Client you need `mobile_app` component to be enabled. If you have `default_config` in your `configuration.yaml` you don't need to add anything. If not - just add (or check if exist) this line to your `configuration.yaml`:

```yaml
mobile_app:
```

Also to make HA Client work outside of your home network [remote access](https://www.home-assistant.io/docs/configuration/remote/) should be configured or [Remote UI](https://www.nabucasa.com/config/remote/) should be used.

[Back to top](#help-pages---what-you-need)

## Android
Minimum supported Android API level is 21. That’s **Android 5.0** and higher.

[Back to top](#help-pages---what-you-need)

### Next > [Connection](/help/connection)
