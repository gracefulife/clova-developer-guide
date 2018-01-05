# Common fields

All content templates contain the following common fields. The level of common fields in content template objects is the top-level.

| Field name        | Type    | Description                     | Provided |
|----------------|---------|-----------------------------|:---------:|
| `actionList[]`     | [ActionObject](/CIC/References/ContentTemplates/Shared_Objects.md#ActionObject) array | Contains a list of actions in the form of [Action URL scheme](#ActionURLScheme) for the client to take. An action can be a responsive action to interact with users. The [CardList](/CIC/References/ContentTemplates/CardList.md) template has this field defined inside the `cardList[]` field. | Conditional |
| `failureMessage` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The message to display in case the client fails to display the content contained in the content template. For instance, if the client does not support the content template version specified by the  `meta.version` field, the client shall display this message instead of displaying the provided content. | Always |
| `meta`             | Object | Contains metadata for the content template. | Always |
| `meta.version`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The version of the content template. | Always |

## Common field example

{% raw %}
```json
{
  "type": "Atmosphere",
  "valueOfAtmosphere": {
    "type": "number",
    "value": "23㎍/㎥"
  },
  ...
  "failureMessage": {
    "type": "string",
    "value": "The current fine dust level for Shinjuku is good"
  },
  "meta": {
    "version": {
      "type": "string",
      "value": "v0.1"
    }
  }
}
```
{% endraw %}

## Action URL scheme {#ActionURLScheme}

The action URL schemes inform the client what action to take.

| Action URL scheme           | Description                                            |
|-----------------------------|------------------------------------------------------------------|
| [clova://app-launch/default-addressbook](#AppLaunchDefaultAddrBook) | Launch the default contacts app   |
| [clova://app-launch/default-browser](#AppLaunchDefaultBrowser)      | Launch the default Web browser |
| [clova://app-launch/default-camera](#AppLaunchDefaultCamera)        | Launch the default camera app   |
| [clova://app-launch/default-email](#AppLaunchDefaultEmail)          | Launch the default mail app    |
| [clova://app-launch/default-gallery](#AppLaunchDefaultGallery)      | Launch the default photo app   |
| [clova://audio-repeat](#AudioRepeat)                                | Play an audio      |
| [clova://device-control](#DeviceControl)                            | Control a certain feature of the client itself |
| [clova://guide/talking](#GuideTalking)     | Provide a guide on using commands                       |
| [clova://naverSearch](#NaverSearch)        | Search a specific keyword on NAVER app                    |
| [clova://naver-maps](#NaverMaps)           | Launch the NAVER Map app                            |
| [clova://ttsRepeat](#TTSRepeat)            | Start TTS (Text To Speech)                     |
| [clova://webview](#Webview)                | Open a webpage in a Webview                          |

### clova://app-launch/default-addressbook {#AppLaunchDefaultAddrBook}

This scheme is for the client to launch the default contacts app. The following is an example of the action URL scheme.

```
clova://app-launch/default-addressbook
```

### clova://app-launch/default-browser {#AppLaunchDefaultBrowser}

This scheme is for the client to launch the default Web browser. The following is an example of the action URL scheme.

```
clova://app-launch/default-browser
```

### clova://app-launch/default-camera {#AppLaunchDefaultCamera}

This scheme is for the client to launch the default camera app. The following is an example of the action URL scheme.

```
clova://app-launch/default-camera
```

### clova://app-launch/default-email {#AppLaunchDefaultEmail}

This scheme is for the client to launch the default mail app. The following is an example of the action URL scheme.

```
clova://app-launch/default-email
```

### clova://app-launch/default-gallery {#AppLaunchDefaultGallery}

This scheme is for the client to launch the default photo app. The following is an example of the action URL scheme.

```
clova://app-launch/default-gallery
```

### clova://audio-repeat {#AudioRepeat}

This scheme is for the client to play an audio file.

| Parameter name    | Description                         | Provided |
|---------------|-----------------------------|:--------:|
| url           | Audio file URL                | Always |

The following is an example of the action URL scheme.

```
clova://audio-repeat?url=http://target.audioFile.url
```

### clova://device-control {#DeviceControl}

This scheme is for the client to control a specific feature or mode of the client.

| Parameter name    | Description                         | Provided |
|---------------|-----------------------------|:--------:|
| command       | Control command <ul><li>BtConnect</li><li>BtDisconnect</li><li>BtStartPairing</li><li>BtStopPairing</li><li>Decrease</li><li>Increase</li><li>LaunchApp</li><li>OpenScreen</li><li>SetValue</li><li>TurnOn</li><li>TurnOff</li></ul>                      | Always |
| target        | Target feature to control <ul><li><code>"airplane"</code>: Airplane mode</li><li><code>"app"</code>: App</li><li><code>"bluetooth"</code>: Bluetooth</li><li><code>"cellular"</code>: Mobile communication</li><li><code>"channel"</code>: TV channel</li><li><code>"flashlight"</code>: Flashlight</li><li><code>"gps"</code>: GPS</li><li><code>"powersave"</code>: Power saving mode</li><li><code>"screenbrightness"</code>: Screen brightness</li><li><code>"soundmode"</code>: Sound mode</li><li><code>"volume"</code>: Speaker volume</li><li><code>"wifi"</code>: WiFi</li></ul> | Always |
| value         | Setting value. This value is being designated when the `command` parameter is a `setValue`. It is also applied when setting speaker volume(`"volume"`) or screen brightness(`"screenbrightness"`) or controlling TV channel(`"channel"`). | Conditional |

The following is examples of the action URL scheme.

```
clova://device-control?command=SetValue&target=volume&value=5
clova://device-control?command=TurnOn&target=flashlight
```

### clova://guide/talking {#GuideTalking}

This scheme is for the client to provide a command helper. The following is an example of the action URL scheme.


```
clova://guide/talking
```

### clova://naverSearch {#NaverSearch}

This scheme is for the client to make a search on the NAVER app.

| Parameter     | Description                         | Provided |
|---------------|-----------------------------|:--------:|
| url           |  The URL of the page to open in the NAVER app | Always |

The following is an example of the action URL scheme.

```
clova://naverSearch?url=http://target.page.url
```

### clova://naver-maps {#NaverMaps}

This scheme is for the client to find routes on the NAVER Map app.

| Parameter     | Description                         | Provided |
|---------------|-----------------------------|:--------:|
| url           | The URL to be opened with the NAVER Map app   | Always |

The following is an example of the action URL scheme.

```
clova://naver-maps?url=http://target.map.url
```

### clova://ttsRepeat {#TTSRepeat}

This scheme is for the client to read out a text.

| Parameter     | Description                         | Provided |
|---------------|-----------------------------|:--------:|
| lang          | The language of the text to be read out <ul><li><code>"ko"</code>: Korean</li><li><code>"en"</code>: English</li></ul> | Always |
| text          | The text to be read out                   | Conditional |

The following is an example of the action URL scheme.

```
clova://ttsRepeat?lang=en&text=hello
```

### clova://webview {#WebView}

This scheme is for the client to open a page in a Webview.

| Parameter     | Description                         | Provided |
|---------------|-----------------------------|:--------:|
| url           | The URL of the page to open              | Always |
| auth_required | Indicates whether authentication is required or not: <ul><li><code>true</code>: Use the Authentication API to open the page.</li><li><code>false</code>: Authentication is not required.</li><li>Undefined: Authentication is not required.</li></ul> | Conditional |

The following is an example of the action URL scheme.

```
clova://webview?url=http://target.page.url&auth_required=true
```
