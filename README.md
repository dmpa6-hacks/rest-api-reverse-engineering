# Reverse Engineering of the Eversolo DMP-A6 REST API

This documentation provides a description of the reverse engineered Eversolo DMP-A6 REST API.

Reverse engineering has been done with the Eversolo Control app for iOS running on a Mac with Apple Silicon processor and Wireshark as network logger.

## REST API

The device listens on port `9529`. All request are done using `HTTP` without encryption.

### Connect to device

**HTTP Method:** `GET`

**URI:** `/ZidooControlCenter/connect?name={Client Name}&uuid={UUID}&tag=0&type=1`

**Reply:**

JSON Object:

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

### Retrieve list of inputs and outputs

**HTTP Method:** `GET`

**URI:** `/ZidooMusicControl/v2/getInputAndOutputList`

**Reply:**

JSON Object:

- "status": HTTP Status (integer)
- "inputData": Array of JSON objects (available inputs)
  - "name": Name of the input (string)
  - "historyName": ???, most likely the same as above (string)
  - "tag": Tag of the input, to be used when setting the input (string)
  - "isEdit": ??? (bool)
  - "index": Index of the input (integer)
  - "icon": URI to retrieve the icon, returns PNG file (string)
  - "selecticon": URI to retrieve the icon for selected state, returns PNG file (string)
- "inputIndex": Index of the currently selected input (integer)
- "outputData": Array of JSON objects (available outputs)
  - "name": Name of the output (string)
  - "tag": Tag of the output, to be used when setting the output (string)
  - "enable": Flag that determines whether the output can be set (bool)
  - "icon": URI to retrieve the icon, returns PNG file (string)
  - "selecticon": URI to retrieve the icon for selected state, returns PNG file (string)
- "outputIndex": 1
- "outputInfo": JSON object (current output parameters)
  - "vidPid": ??? (string)
  - "name": ??? (string)
  - "format": Output format (string)
  - "sampleRate": Sample rate (string)
  - "infolist": Array of JSON objects (title/value pairs)
    - "title": Title for detail (string)
    - "value": Value of detail (string
  - "isConnect": ??? (bool)
  - "setUrl": URI to set something (???) (string)
  - "title": ??? (string)
  - "option": ??? (integer)

### Set the input

**HTTP Method:** `GET`

**URI:** `/ZidooMusicControl/v2/setInputList?tag=RCA&index=4`

**Reply:** Same as for getInputAndOutputList

### Set the output

**HTTP Method:** `GET`

**URI:** `/ZidooMusicControl/v2/setOutInputList?tag=XLR&index=0`

**Reply:** Same as for getInputAndOutputList

### Play/Pause

**HTTP Method:** `GET`

**URI:** `/ZidooMusicControl/v2/playOrPause`

**Reply:**

JSON Object:

- "status": HTTP Status (integer)

### Volume Up

**HTTP Method:** `GET`

**URI:** `/ZidooControlCenter/RemoteControl/sendkey?key=Key.VolumeUp`

**Reply:**

JSON Object:

- "status": HTTP Status (integer)

### Volume Down

**HTTP Method:** `GET`

**URI:** `/ZidooControlCenter/RemoteControl/sendkey?key=Key.VolumeDown`

**Reply:**

JSON Object:

- "status": HTTP Status (integer)

### Play Next

**HTTP Method:** `GET`

**URI:** `/ZidooMusicControl/v2/playNext`

**Reply:**

JSON Object:

- "status": HTTP Status (integer)

### Play Previous

**HTTP Method:** `GET`

**URI:** `/ZidooMusicControl/v2/playLast`

**Reply:**

JSON Object:

- "status": HTTP Status (integer)

### Change VU Display

**HTTP Method:** `GET`

**URI:** `/ZidooMusicControl/v2/changVUDisplay`

**Reply:**

JSON Object:

- "status": HTTP Status (integer)

### Retrieve Power Options

**HTTP Method:** `GET`

**URI:** `/ZidooMusicControl/v2/getPowerOption`

**Reply:**

JSON Object:

- "status": HTTP Status (integer)
- "data": Array of JSON Objects (power options)
  - "name": Option name (string)
  - "tag": Tag of the power option to be used with the `setPowerOption` API (string)

### Set Power Option

**HTTP Method:** `GET`

**URI:** `/ZidooMusicControl/v2/setPowerOption?tag={power_option_tag}`

`{power_option_tag}` is one of the tags returned by the `getPowerOption` API

**Reply:**

JSON Object:

- "status": HTTP Status (integer)
