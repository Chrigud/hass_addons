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
3. a. Enable the webserver (in rcpservers.conf). Enable the webserver in port 2001 and disable RPC on that port.
3. b. If you want to use the HM-CFG-USB 2 stick, add the HM-CFG-USB configuration to families/homematicbidcos.conf (see below). Then you can add the hmcfglan type to HomematicBidcos with the hmland ID. You may also want to set centralAddress and rfKey. If you come from an existing setup, it is important to reuse the same rfKey if devices are already paired. If you want to switch to a new key, you must define oldRfKey!
3. c. If you want to use the MAX!Cube as CUNX (with a-culfw), use the CUNX configuration below. You may also change centralAddress, but be careful if devices are paired with a different central address.
4. Restart the addon
5. a. For communicaton with hass, add a CCU config to your /config/configuration.yaml (Includeing the Port 2002 for RPC Communication)
5. b. One can also enable MQTT (in mqtt.conf) and then setup the devices with the MQTT plugin and device IDs. You probably also need to set the IP in brokerHostname. And set the username and password for protection.
6. A nice addition to homegear is the Homematic-Manager, which can access homegear and the devices via RPC and offers additional functionality (e.g. configure shutter reference running time). It requires RPC port 2001 to be active.

# WebGui

The Admin GUI is available via "http://your-hass:2001/admin"

# Restricions

You can't use the CLI Configuration. You can add devices via ADMIN-UI (tested with MAX! and Homematic)

# Examples

#### HM-CFG-USB - families/homematicbidcos.conf
```conf
#######################################
############# HM-CFG-USB ##############
#######################################
[HM-CFG-USB]
id = hmland
#default = true
deviceType = hmcfglan
host = <ip>
port = 1234
responseDelay = 60
```

```conf
#### CUNX - MAX - families/max.conf
#######################################
################ CUNX  ################
#######################################
[CUNX]
id = CUL_MAX
default = true
deviceType = cunx
host = <ip>
port = 2323
responseDelay = 40
```

#### configuration.yaml

```yaml
#Homematic (Homegear)
homematic:
  interfaces:
    wireless:
      host: 10.4.4.113
      resolvenames: metadata
      port: 2002
```
