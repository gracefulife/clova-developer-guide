# Common fields
All content templates may have the common fields as below. The common fields are located at the top level property of all the others.

| Field name        | Type    | Field description                     | Required |
|----------------|---------|-----------------------------|---------|
| `actionList[]`     | [ActionObject](/CIC/References/ContentTemplates/Shared_Objects.md#ActionObject) array | Users should be provided with content template so that they may respond to the user interactions such as UI touch. The list of response actions([Action URL scheme](#ActionURLScheme)) should be conveyed to the user interaction through this field. [CardList](/CIC/References/ContentTemplates/CardList.md) type of content template can be defined at the sub level of `cardList[]` field.  | No |
| `failureMessage[]` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Includes the message information in case the content template cannot be expressed on UI. | Yes |
| `meta`             | object | Includes meta information related to content template. | Yes |
| `meta.version`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Contains content template version information. | Yes |

## An example of the common fields

{% raw %}
```json
// When using general content template

{
  "bgUrl": {
    "type": "url",
    "value": ""
  },
  ...
  "type": "Text",
  "actionList": [
    {
      "type" : "action",
      "value" : "clova://ttsRepeat?lang=ko&text=1달러 환율입니다."
    }
  ],
  "failureMessage": {
    "type": "string",
    "value": "정보를 확인하는데 실패했습니다."
  },
  "meta" : {
    "version" : {
      "type" : "string",
      "value" : "1.0"
    }
  }
}

// When using Card List type
{
  "subType": "",
  "type": "CardList",
  "cardList": [
    {
      "title": {
        "type": "string",
        "value": "인카네이트"
      },
      ...
      "actionList": [
        {
          "type" : "action",
          "value" : "clova://naverSearch?url=https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=+%ec%98%81%ed%99%94"
        }
      ]
    },
    {
      "title": {
        "type": "string",
        "value": "링스"
      },
      ...
      "actionList": [
        {
          "type" : "action",
          "value" : "clova://naverSearch?url=https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=+%ec%98%81%ed%99%94"
        }
      ]
    },
    ...
  ],
  "failureMessage": {
    "type": "string",
    "value": "영화 정보를 확인하는데 실패했습니다."
  },
  "meta" : {
    "version" : {
      "type" : "string",
      "value" : "1.0"
    }
  }
}
```
{% endraw %}

## Action URL scheme {#ActionURLScheme}
The following action URL schemes defined in the `actionList` field inform the client what actions to take.

| Action URL scheme           | Description                                                              |
|-----------------------------|------------------------------------------------------------------|
| [clova://app-launch/default-addressbook](#AppLaunchDefaultAddrBook) | An action to execute basic address app   |
| [clova://app-launch/default-browser](#AppLaunchDefaultBrowser)      | An action to execute basic web browser |
| [clova://app-launch/default-camera](#AppLaunchDefaultCamera)        | An action to execute basic camera app   |
| [clova://app-launch/default-email](#AppLaunchDefaultEmail)          | An action to execute basic email app    |
| [clova://app-launch/default-gallery](#AppLaunchDefaultGallery)      | An action to execute basic gallery app   |
| [clova://audio-repeat](#AudioRepeat)                                | An action to play an audio content     |
| [clova://device-control](#DeviceControl)                            | An action to control a device       |
| [clova://guide/talking](#GuideTalking)     | An action to provide a command helper                              |
| [clova://naverSearch](#NaverSearch)        | An action to search a specific keyword on Naver app                    |
| [clova://naver-maps](#NaverMaps)           | An action to execute Naver Map app                            |
| [clova://ttsRepeat](#TTSRepeat)            | An action to execute Text To Speech                     |
| [clova://webview](#Webview)                | An action to open a webpage through WebView                          |

### clova://app-launch/default-addressbook {#AppLaunchDefaultAddrBook}

This scheme is for the client to launch the basic address app. The following is an example for the action URL scheme.

```
clova://app-launch/default-addressbook
```

### clova://app-launch/default-browser {#AppLaunchDefaultBrowser}

This scheme is for the client to launch the basic web browser. The following is an example for the action URL scheme.

```
clova://app-launch/default-browser
```

### clova://app-launch/default-camera {#AppLaunchDefaultCamera}

This scheme is for the client to launch the basic camera app. The following is an example for the action URL scheme.

```
clova://app-launch/default-camera
```

### clova://app-launch/default-email {#AppLaunchDefaultEmail}

This scheme is for the client to launch the basic email app. The following is an example for the action URL scheme.

```
clova://app-launch/default-email
```

### clova://app-launch/default-gallery {#AppLaunchDefaultGallery}

This scheme is for the client to launch the basic gallery app. The following is an example for the action URL scheme.

```
clova://app-launch/default-gallery
```

### clova://audio-repeat {#AudioRepeat}

This scheme is for the client to play an audio file.

| Parameter name    | Description                         | Required |
|---------------|-----------------------------|--------|
| url           | Audio file URL                | Yes |

The following is an example for the action URL scheme.

```
clova://audio-repeat?url=http://target.audioFile.url
```

### clova://device-control {#DeviceControl}

This scheme is for the client to control a specific feature of client.

| Parameter name    | Description                         | Required |
|---------------|-----------------------------|--------|
| command       | Control command <ul><li>BtConnect</li><li>BtDisconnect</li><li>BtStartPairing</li><li>BtStopPairing</li><li>Decrease</li><li>Increase</li><li>LaunchApp</li><li>OpenScreen</li><li>SetValue</li><li>TurnOn</li><li>TurnOff</li></ul>                      | Yes |
| target        | Target to control. <ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"app"</code>: App</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"cellular"</code>: Mobile communication</li><li><code>"channel"</code>: TV channel</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"powersave"</code>: Power saving mode</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"soundmode"</code>: Sound mode</li><li><code>"volume"</code>: Speaker volume</li><li><code>"wifi"</code>: Wireless LAN</li></ul> | Yes |
| value         | Setting value. This value is being designated when the `command` parameter is a `setValue`. It is also applied when setting speaker volume(`"volume"`) or screen brightness(`"screenbrightness"`) or controlling TV channel(`"channel"`). | No |

The following is an example for the action URL scheme.

```
clova://device-control?command=SetValue&target=volume&value=5
clova://device-control?command=TurnOn&target=flashlight
```

### clova://guide/talking {#GuideTalking}

This scheme is for the client to provide a command helper. The following is an example for the action URL scheme.


```
clova://guide/talking
```

### clova://naverSearch {#NaverSearch}

This scheme is for the client to search on Naver app.

| Parameter name    | Description                         | Required |
|---------------|-----------------------------|--------|
| url           |  URL of the page you are about to open through Naver app | Yes |

The following is an example for the action URL scheme.

```
clova://naverSearch?url=http://target.page.url
```

### clova://naver-maps {#NaverMaps}

This scheme is for the client to find a way by executing Naver Map app.

| Parameter name    | Description                         | Required |
|---------------|-----------------------------|--------|
| url           | An URL opened via the Naver Map app   | Yes |

The following is an example for the action URL scheme.

```
clova://naver-maps?url=http://target.map.url
```

### clova://ttsRepeat {#TTSRepeat}

This scheme is for the client to read out a specific text.

| Parameter name    | Description                         | Required |
|---------------|-----------------------------|--------|
| lang          | TTS(Text to Speech) target language. <ul><li><code>"ko"</code>: Korean</li><li><code>"en"</code>: English</li></ul> | Yes |
| text          | The text to be read out                   | No |

The following is an example for the action URL scheme.

```
clova://ttsRepeat?lang=en&text=hello
```

### clova://webview {#WebView}
This scheme is for the client to open a specific page through WebView.

| Parameter name    | Description                         | Required |
|---------------|-----------------------------|--------|
| url           | URL of the target page               | Yes |
| auth_required | Whether authentication is required or not. If the parameter is `true`, use authentication API to open the target page. If it is `false` or unmentioned, authentication is not required. | No |

The following is an example for the action URL scheme.

```
clova://webview?url=http://target.page.url&auth_required=true
```
