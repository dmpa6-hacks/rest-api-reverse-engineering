# Reverse Engineering of the Eversolo DMP-A6 REST API

This documentation provides a description of the reverse engineered Eversolo DMP-A6 REST API.

Reverse engineering has been done with the Eversolo Control app for iOS running on a Mac with Apple Silicon processor and Wireshark as network logger.

## REST API

The device listens on port `9529`. The prefix for each REST API call is `/ZidooControlCenter`. All request are done using `HTTP` without encryption.

### Connect to device

**URI:**

`/connect?name={Client Name}&uuid={UUID}&tag=0&type=1`

**Reply:**

JSON Structure:

- "status": HTTP Status (integer)
- "model": Model name (string)
- "ip": IP address (string)
- "net_mac": MAC address of LAN port (string)
- "dType": 0 (???)
- "duuid": MAC address of LAN port (string)
- "firmware": Installed firmware version, e.g. "v1.2.30" (string)
- "ram": RAM size in GB, e.g. "4.0G" (string)
- "flash": Flash memory size, e.g. "32.0G" (string)
- "androidversion": Installed Android version (string)
- "wif_mac": MAC address of Wifi port (string)
- "language": Configured language, e.g. "de" (string)
- "ableRemoteBoot": Boot can be triggered remotely (bool)
- "ableRemoteShutdown": Shutdown can be triggered remotely (bool)
- "ableRemoteReboot": Reboot can be triggered remotely (bool)
- "ableRemoteSleep": Sleep can be triggered remotely (bool)
- "ableMusicService": ??? (bool)
- "ableMusicTest": ??? (bool)
- "hasDspSetting": ??? (bool)
- "nationcode": ???, e.g. "276" (string)
- "uuid": ??? (UUID as string)
- "device": Object with the following properties
  - "type": ??? (integer)
  - "uuid": ??? same as above (UUID as string)
  - "name": Name of the device (string)
  - "sceneCode": ??? (integer)
  - "scene": ??? (string)
  - "host": IP address (string)
  - "port": Port of the REST endpoint (integer)
  - "ableRemoteBoot": Boot can be triggered remotely (bool)
  - "ableRemoteShutdown": Shutdown can be triggered remotely (bool)
  - "ableRemoteReboot": Reboot can be triggered remotely (bool)
  - "ableRemoteSleep": Sleep can be triggered remotely (bool)
  - "ableMusicService": ??? (bool)
  - "ableMusicTest": ??? (bool)
  - "nationcode": ???, e.g. "276" (string)
  - "language": Configured language, e.g. "de" (string)
  - "hasDspSetting": ??? (bool)
