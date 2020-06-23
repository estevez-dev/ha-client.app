# Sensor for next Android alarm
Nearest alarm set on your phone will now be sent to Home Assistant as sensor state. You can find new sensor entity in your Home Assistant -> **Configuration** -> **Integrations** -> **Mobile App**.

Example sensor state: `2020-06-24 09:00:00`

For easy automations creating there is additional `attributes` in sensor containing different time formats:
```
date: '2020-06-24'
time: '09:00:00'
timestamp: 1592978400000
```
