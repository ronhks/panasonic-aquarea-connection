:information_source: :one: HA forum available [there](https://community.home-assistant.io/t/panasonic-aquarea-heat-pump-integration) 

:information_source: :two:  If you would like to use a full integration, please check [Carlos's](https://github.com/cjaliaga) full [HomeAssistant integration](https://github.com/cjaliaga/home-assistant-aquarea)!

# Panasonic Aquaera Smart Cloud integration with MQTT
At home I have a Home Assistant and I would like control my Panasonic Aquarea Heatpump.

This project a transformation layer from [Panasonic Smart Cloud](https://aquarea-smart.panasonic.com/) with [MQTT](https://en.wikipedia.org/wiki/MQTT). 

If you satisfied, thanks for buying a coffee for me :)

[!["Buy Me A Coffee"](https://www.buymeacoffee.com/assets/img/custom_images/orange_img.png)](https://www.buymeacoffee.com/zsoltdenes)

### Requirements
* MQTT server
* [Panasonic Smart Cloud](https://aquarea-smart.panasonic.com/) registration
* [Panasonic Aquarea Wifi Module - Panasonic CZ-TAW1](https://www.panasonicproclub.com/uploads/PL/catalogues/CZ-TAW1_quick%20guide.pdf)

## How to start 
### Natively
#### Make
```shell
make
```
#### Configure
Create a config file copy as `config` from [config.example](./etc/config.example)

The config have to be defined in `PANASONIC_AQUAREA_SMART_CLOUD_MQTT_CONFIG` environment variable.

If the environment variable not set, the default is: `etc/config`
#### Run
```sh
$ PANASONIC_AQUAREA_SMART_CLOUD_MQTT_CONFIG="CONFIG_FILE_LOCATION" bin/OS/panasonic-aquarea-smart-cloud-mqtt-OS-ARCH
```
### As continer
#### Pull
```shell
$ docker pull ronhks/panasonic-aquarea-smart-cloud-mqtt
```
#### Run
```sh
$ docker run --name panasonic-aquarea-smart-cloud-mqtt -v HOST_OS_CONFIG_LOCATION/:/app/etc ronhks/panasonic-aquarea-smart-cloud-mqtt
```

As daemon add `-d` option
## How to use
The MQTT topic are under the `MqttTopicRoot`.
### Read values
* `/outdoor/temp/now` - Outdoor temp
* `/heat/temp/max` - Heating max. temp 
* `/heat/temp/min` - Heating min. temp
* `/heat/operation` - Heating operation status
  * `0` - OFF
  * `1` - ON
* `/heat/operation/set` - Change Heating operation status
  * `OFF` - OFF
  * `ON` - ON
* `/water/temp/now` - Actual Hot Water temp
* `/water/temp/max` - Hot water max. temp.
* `/water/temp/min` - Hot water min. temp.
* `/water/operation` - Hot water operation status
  * `0` - OFF
  * `1` - ON
* `/water/operation/set` - Change Hot water operation status
  * `OFF` - OFF
  * `ON` - ON
* `/operation` - Device operation status
  * `0` - OFF
  * `1` - ON
* `/operation/set` - Device operation status
  * `OFF` - OFF
  * `ON` - ON

### Change values
* `/water/temp/set` - set the HOT WATER temp. 
  * sample REQUEST JSON:
    ```json
    {
      "newTemp" : 42
    }
    ```
* `/water/operation/on` - Turn ON the Hot Water
* `/water/operation/off` - Turn OFF the Hot Water
* `/heat/operation/on` - Turn ON the heating
* `/heat/operation/off` - Turn OFF the heating
* `/operation/on` - Turn ON the device
* `/operation/off` - Turn OFF the device

* `/heat/temp/set` - set the HEAT water temp (if this is customizable from your heat pump installer settings). The same temp will be set for first and second zone.
  * sample REQUEST JSON:
    ```json
    {
      "newTemp" : 42
    }
    ```

## Contributing
Welcome all type of contributing! :)

#### 3rd party libs
**Thanks for**
* [BurntSushi/toml](https://github.com/BurntSushi/toml) for easier config handling
* [eclipse/paho.mqtt.golan](https://github.com/eclipse/paho.mqtt.golan) for MQTT handling
* [sirupsen/logrus](https://github.com/sirupsen/logrus) for easier logging
