---
title: "Samsung Smart TV"
description: "Instructions on how to integrate a Samsung Smart TV into Home Assistant."
logo: samsung.png
ha_category:
  - Media Player
ha_release: 0.13
ha_iot_class: Local Polling
---

The `samsungtv` platform allows you to control a [Samsung Smart TV](http://www.samsung.com/uk/consumer/tv-audio-video/televisions/).

### Setup

When the TV is first connected, you will need to accept Home Assistant on the TV to allow communication.

### Configuration

To add a TV to your installation without relying on the [discovery component](/integrations/discovery/), add the following to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
media_player:
  - platform: samsungtv
    host: IP_ADDRESS
```

{% configuration %}
host:
  description: "The IP of the Samsung Smart TV, e.g., `192.168.0.10`."
  required: true
  type: string
port:
  description: The port of the Samsung Smart TV. If set to 8001, the new websocket connection will be used (required for 2016+ TVs) - for installs other than Hass.io or Docker you may need to install a Python package, see below.
  required: false
  type: integer
  default: 55000
name:
  description: The name you would like to give to the Samsung Smart TV.
  required: false
  type: string
timeout:
  description: The timeout for communication with the TV in seconds.
  required: false
  type: time
  default: 0 (no timeout)
mac:
  description: "The MAC address of the Samsung Smart TV, e.g., `00:11:22:33:44:55:66`. Required for power on support via wake on lan."
  required: false
  type: string
{% endconfiguration %}

Currently known supported models:

- C7700
- D5500
- D6300SF
- D6500
- D6505
- D7000
- D8000
- EH5300
- EH5600
- ES5500
- ES5700
- ES6300
- ES6800
- F4580
- F6300
- F6400
- F6400AF
- F6500
- F7000
- F8000BF
- K5579 (port must be set to 8001, On/Off, Forward/Backward, Volume control, but no Play button)
- K5600AK (partially supported, turn on works but state is not updated)
- K6500AF (port must be set to 8001)
- KS7005 (port must be set to 8001, MAC address must be provided, On/Off, Volume are OK, no channel change)
- KS7502 (port must be set to 8001, turn on doesn't work, turn off works fine)
- KS8000 (port must be set to 8001)
- KS8005 (port must be set to 8001)
- KS8500 (port must be set to 8001)
- KU6020 (port must be set to 8001)
- KU6100 (port must be set to 8001)
- KU6290 (port must be set to 8001)
- KU6400U (port must be set to 8001)
- KU7000 (port must be set to 8001)
- M5620 (port must be set to 8001)
- MU6170UXZG (port must be set to 8001)
- NU7090 (port must be set to 8801, On/Off, MAC must be specified for Power On)
- NU7400 (port set to 8001)
- NU8000
- U6000 (port must be set to 8001)
- U6300 (port must be set to 8001)
- UE6199UXZG (port must be set to 8001, On/Off, Forward/Backward, Volume control, but no Play button)
- UE65KS8005 (port must be set to 8001, On/Off, Forward/Backward, Volume are OK, but no Play button)
- UE49KU6470 (port must be set to 8001, On/Off, Forward/Backward, Volume are OK, but no Play button)
- UE46ES5500 (partially supported, turn on doesn't works)

Currently tested but not working models:

- J5200 - Unable to see state and unable to control
- J5500 - State is always "on" and unable to control (but port 8001 *is* open)
- J6200 - State is always "on" and unable to control (but port 8001 *is* open)
- J6300 - State is always "on" and unable to control (but port 8001 *is* open)
- JS8005 - State tracking working but unable to control (but port 8001 *is* open)
- JS9000 - State is always "on" and unable to control (but port 8001 *is* open)
- JS9500 - State is always "on" and unable to control (but port 8001 *is* open)
- JU6800 - Unable to see state and unable to control
- JU7000 - Unable to see state and unable to control (but port 8001 *is* open)
- JU7500 - Unable to see state and unable to control
- MU6125 - Unable to see state and unable to control (Tested on UE58MU6125 on port 8001 and 8801)
- MU6300 - Port set to 8001, turning on works, status not working reliably, turning off is not permanent (it comes back on)
- Q7F - State is always "off" and unable to control via port 8001.

None of the 2014 (H) and 2015 (J) model series (e.g., J5200) will work, since Samsung have used a different (encrypted) type of interface for these.

If your model is not on the list then give it a test, if everything works correctly then add it to the list on
[GitHub](https://github.com/home-assistant/home-assistant.github.io/tree/current/source/_components/samsungtv.markdown).
The first letter (U, P, L, H & K) represent the screen type, e.g., LED or Plasma. The second letter represents the region, E is Europe, N is North America and A is Asia & Australia. The two numbers following that represent the screen size.
If you add your model remember to remove these first 4 characters before adding to the list.

Changing channels can be done by calling the `media_player.play_media` service
with the following payload:

```javascript
{
  "entity_id": "media_player.office_tv",
  "media_content_id": "590",
  "media_content_type": "channel"
}
```

Currently the ability to select a source is not implemented.

### Hass.io

No additional actions are required

### Docker

No additional actions are required

### Hassbian

You will need to activate the venv and install the websocket library:

```bash
sudo -u homeassistant -H -s
source /srv/homeassistant/bin/activate
pip3 install websocket-client
```
### Other install methods

You will need to install the `websocket-client` Python package in your Home Assistant install. This will probably be done with:

```bash
pip3 install websocket-client
```

Remembering to activate your venv if you're using a venv install.
