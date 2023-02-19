# Homegear4Homeassistant

This addon integrated Homegear and hmland into Home Assistant.

This plugin is based on the original Docker Image from the Homegear project (https://github.com/Homegear/Homegear-Docker/tree/master/stable) and the Homegear4Homeassistant plugin from BiasF (https://github.com/BiasF/homegear4homeassistant/tree/main/homegear4homeassistant).
It already extended the Homegear image, but was outdated and missing the hmland integration, that I needed.

Feel free to use the addon, but keep in mind it comes absolutely without warranty and support \
(of course feel free to give feedback on github, I will do my best to fix problems and update the repo).

# Usage

1. Add this repo to your HASS Repomanager (Write the repo URL in lowercase and don't use Captial letters)
2. Install the Plugin and start it (There are no HASSIO Addon Configuration parameters yet)
3. At first boot, the Addon creates a homegear directory in your config folder. You have to configure it like a stand alone homegear system.
4. Restart the addon
5. For communicaton with hass, add a CCU config to your /config/configuration.yaml (Includeing the Port 2001 for RPC Communication)
6. (optional) Alternatively one can also access the devices via MQTT

# WebGui

The Admin GUI is available via "http://your-hass:2001/admin"

# Restricions

You can't use the CLI Configuration. You can add devices via ADMIN-UI (tested with MAX! and Homematic)

# Examples

#### configuration.yaml

```yaml
#Homematic (Homegear)
homematic:
  interfaces:
    wireless:
      host: 10.4.4.113
      resolvenames: metadata
      port: 2001
```
