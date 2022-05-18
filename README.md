<h1 style="font-weight:normal">
  &nbsp;WAGO PFC KBUS API Installer v2.0.0 &nbsp;
</h1>

An open source MQTT driver for WAGO PFC controllers backplane.

This project is still in beta - please use at your own risk and post any bugs to [issues](https://github.com/jessejamescox/kbus-daemon-installer/issues)

### Version 2.0 introduces updates that will break version 1.X.X. of the node-red-contrib-wago nodes for Node-RED.
<br>

# Features

- KBUS connects directly to MQTT broker either onboard the controller or externally
- Status and error messages are sent under <NodeID>/kbus/status topic
- KBUS process data is transmitted under <NodeID>/kbus/event <inputs/outputs> topic
- Supoprt all WAGO "simple" modules, analog and digital
- Entirely event driven I/O bus minimizes network stress
- Very low CPU resource usage

# Get started

Install the driver on your controller. This is done with the following command:

`wget https://github.com/jessejamescox/kbus-api-installer/archive/refs/heads/main.zip && unzip main.zip && sh kbus-api-installer-main/installer.sh`

# The API

## KBUS input events:

Input events will be transmitted upon change-of-state. This will be a JSON structured message the the module position and channel position. The output structure follows the formatting for state.reported For example:

```
{
  "state": {
    "reported": {
      "controller": {
        "modules": {
          "module1": {
            "channels": {
              "channel1": {
                "value": 123
              }
            }
          }
        }
      }
    }
  }
}
```

## KBUS output commands:

Similar to the input structure, you can command outputs over MQTT by passing a JSON object with the following structure:

```
{
  "state": {
    "desired": {
      "controller": {
        "modules": {
          "module2": {
            "channels": {
              "channel1": {
                "value": true
              }
            }
          }
        }
      }
    }
  }
}
```

## KBUS chnnel configuration:

Channel parameters can be configured by passing values as well.  Here is an example for setting a deadband and a label to the specific channel:

```
{
  "state": {
    "desired": {
      "controller": {
        "modules": {
          "module3": {
            "channels": {
              "channel1": {
                "label": "tankLevel_4-20ma",
                "deadband": 25
              }
            }
          }
        }
      }
    }
  }
}
```

Currently the only supported configurations are deadband for analog inputs, and label for all channels.   More are planned with future development.

# Requirements

- WAGO PFC with firmware 19

# Development

This project is open source and can be modified. See here for the development repo [kbus-api source](https://github.com/jessejamescox/wago-kbus-daemon) for more information.

# Changelog

- 5-18-2022
- Updated to firmware 19
- Added Power Measurement Module

# License

kbus-daemon-installer is under the MIT license. See the [LICENSE](https://github.com/jessejamescox/kbus-daemon-installer/blob/main/LICENSE.md) for more information.

# Links

- [Jesse Cox YouTube](https://www.youtube.com/channel/UCXEwdiyGgzVDJD48f7rWOAw)
- [Jesse Cox LinkedIn](https://www.linkedin.com/in/jesse-cox-90535110/)

```

```
