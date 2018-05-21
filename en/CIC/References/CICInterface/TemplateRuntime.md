# TemplateRuntime

The TemplateRuntime namespace is used when the client or CIC requests or sends the playback metadata to display on the media player. The [`AudioPlayer`](/CIC/References/CICInterface/AudioPlayer.md) interface must be used when performing tasks related to the information required for the actual audio stream playback and the `TemplateRuntime` interface must be used when performing tasks related to the playback metadata information such as play list, album image, or lyrics. Through this, the client can retrieve the playback metadata of another client device as well as itself and also provide the information to the user.

| Message name         | Type  | Description                                   |
|------------------|-----------|---------------------------------------------|
| [`ExpectRequestPlayerInfo`](#ExpectRequestPlayerInfo)  | Directive | Instructs the client to request the playback metadata. Upon receiving the directive, the client must send the [`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo) event to CIC. |
| [`LikeCommandIssued`](#LikeCommandIssued)              | Event     | Reports to CIC that the user pressed the Like button on the client device for a specific media. |
| [`RenderPlayerInfo`](#RenderPlayerInfo)                | Directive | Instructs the client to display the sent playback metadata such as a playlist, album image, and lyrics on the media player. |
| [`RequestPlayerInfo`](#RequestPlayerInfo)              | Event     | Requests CIC for playback metadata such as a playlist, album image, and lyrics to display on the media player. |
| [`UnlikeCommandIssued`](#UnlikeCommandIssued)          | Event     | Reports to CIC that the user pressed the Unlike button on the client device for a specific media. |

## ExpectRequestPlayerInfo directive {#ExpectRequestPlayerInfo}

Instructs the client to request playback metadata such as play list, album image, and lyrics. Upon receiving the directive, the client must send the [`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo) event to CIC.

### Payload fields

None

### Message example
{% raw %}

```json
{
  "directive": {
    "header": {
      "namespace": "TemplateRuntime",
      "name": "ExpectRequestPlayerInfo",
      "dialogRequestId": "9d7dc3ca-17ff-4df9-9800-91736ba2a3b6",
      "messageId": "46ccdf6c-609a-43a5-91c4-7a43b961f0c0"
    },
    "payload": {}
  }
}
```

{% endraw %}

### See also
* [`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo)

## LikeCommandIssued event {#LikeCommandIssued}
Reports to CIC that the user pressed the Like button on the client device for a specific media. Upon receiving the event, CIC sends the appropriate directive to the client.


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `token`    | string  | The token of the media content. Make sure to enter the token value provided in the `playableItems[].token` field of the [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo) directive. | Required |

### Remarks
* The button on the client device can either be a physical button or a software button like a widget button on a music player.

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "TemplateRuntime",
      "name": "LikeCommandIssued",
      "messageId": "2fcb6a62-393d-46ad-a5c4-b3db9b640045"
    },
    "payload": {
      "token": "eJyr5lIqSSyITy4tKs4vUrJSUE"
    }
  }
}
```
{% endraw %}

### See also
* [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo)
* [`TemplateRuntime.UnlikeCommandIssued`](#UnlikeCommandIssued)

## RenderPlayerInfo directive {#RenderPlayerInfo}

Instructs the client to display the sent playback metadata such as a playlist, album image, and lyrics on the media player. If the user has requested to play music, the client plays the media by receiving the [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) directive. If necessary, a client with a display may have to express the information related to playback on the media player. For this process, the playback metadata can be requested to CIC using the [`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo) event and the `TemplateRuntime.RenderPlayerInfo` directive is returned. The `TemplateRuntime.RenderPlayerInfo` directive contains playback metadata on the media to play now and media to play later. The client is able to display metadata and play list of the currently playing media by providing the playback metadata of the `TemplateRuntime.RenderPlayerInfo` directive to the user. It also provides the base data (`token`) that can process when the user has request to play specific media in the playlist, or to perform actions such as like ([`TemplateRuntime.LikeCommandIssued`](#LikeCommandIssued)) or unlike ([`TemplateRuntime.UnlikeCommandIssued`](#UnlikeCommandIssued)).

### Payload fields
| Field name       | Data type    | Description                     | Included |
|---------------|---------|-----------------------------|:---------:|
| `displayType`               | string | Display format of the media content.<ul><li><code>"list"</code>: Display a list</li><li><code>"single"</code>: Display a single item</li></ul>       | Always |
| `controls[]`                | object array | The object array that has the button information that the client must display on the media player.             | Always |
| `controls[].enabled`        | boolean      | Indicates whether the buttons specified in the `controls[].name` must be enabled from the media player.<ul><li><code>true</code>: Enable</li><li><code>false</code>: Disable</li></ul>  | Always  |
| `controls[].name`           | string       | The button name. Available values are:<ul><li><code>"NEXT"</code>: Next</li><li><code>"PLAY_PAUSE"</code>: Play/Pause</li><li><code>"PREVIOUS"</code>: Previous</li></ul>  | Always  |
| `controls[].selected`       | boolean      | Indicates whether the media content is selected. This value can be used for displaying user preferences. For example, if this value is set as `true`, the content must be expressed on the relevant UI of the media player since the user has selected it as a preference. <ul><li><code>true</code>: Selected</li><li><code>false</code>: Not selected</li></ul> | Always  |
| `controls[].type`           | string       | The type of button. Currently, only the `"BUTTON"` value is available.  | Always |
| `playableItems[]`           | object array | The object array that has the list of media contents that can be played. This field can be an empty array.  | Always |
| `playableItems[].artImageUrl`  | string    | The URL of the image on the media content. This URL is the location of the album cover image or other relevant icons.      | Conditional |
| `playableItems[].controls[]`                | object array  | The object array of button information that must be displayed when playing a specific media content. This object array is omissible.  | Conditional |
| `playableItems[].controls[].enabled`        | boolean      | Indicates whether the buttons specified in the `playableItems[].controls[].name` must be enabled from the media player.<ul><li><code>true</code>: Enable</li><li><code>false</code>: Disable</li></ul>  | Always  |
| `playableItems[].controls[].name`           | string       | The button name. Available values are:<ul><li><code>"NEXT"</code>: Next</li><li><code>"PLAY_PAUSE"</code>: Play/Pause</li><li><code>"PREVIOUS"</code>: Previous</li></ul>  | Always  |
| `playableItems[].controls[].selected`       | boolean      | Indicates whether the media content is selected. This value can be used for displaying user preferences. For example, if this value is set as `true`, the content must be expressed on the relevant UI of the media player since the user has selected it as a preference. <ul><li><code>true</code>: Selected</li><li><code>false</code>: Not selected</li></ul> | Always  |
| `playableItems[].controls[].type`           | string       | The type of button. Currently, only the `"BUTTON"` value is available.  | Always |
| `playableItems[].headerText`       | string        | The text field used mainly to indicate the title of current play list.                                                | Conditional  |
| `playableItems[].lyrics[]`         | object array  | The object array that has the lyrics information.                                                            | Conditional  |
| `playableItems[].lyrics[].data`    | string        | The lyrics data. Either this field or the `playableItems[].lyrics[].url` field exists.              | Conditional  |
| `playableItems[].lyrics[].format`  | string        | The format of the lyrics data.<ul><li><code>"LRC"</code>: <a href="https://en.wikipedia.org/wiki/LRC_(file_format)" target="_blank">LRC format</a></li><li><code>"PLAIN"</code>: Plain text format</li></ul>  | Always  |
| `playableItems[].lyrics[].url`     | string        | The URL of the lyrics data. Either this field or the `playableItems[].lyrics[].data` field exists.        | Conditional  |
| `playableItems[].showAdultIcon`    | boolean       | Indicates whether to display the icon for adult media.<ul><li><code>true</code>: Must be displayed.</li><li><code>false</code>: Must not be displayed.</li></ul>   | Always  |
| `playableItems[].titleSubText1`    | string        | The text field used mainly to indicate the name of the artist.                                                          | Always |
| `playableItems[].titleSubText2`    | string        | The text field used mainly to indicate the name of the album.                                                      | Conditional |
| `playableItems[].titleText`        | string        | The text field used mainly to indicate the title of the currently playing music.                                                         | Always  |
| `playableItems[].token`            | string        | The token of the media content.                                                                     | Always |
| `provider`                         | object        | The information of the media content provider.                                                         | Conditional |
| `provider.logoUrl`                 | string        | The logo image URL of the media content provider.                                                         | Conditional |
| `provider.name`                    | string        | The name of the media content provider.                                                                   | Always  |
| `provider.smallLogoUrl`            | string        | The URL of the small logo image of the media content provider.                                                | Conditional |

### Message example
{% raw %}

```json
// Example: The audio stream that can be played only with the stream URL
{
  "directive": {
    "header": {
      "namespace": "AudioPlayer",
      "name": "Play",
      "dialogRequestId": "34abac3-cb46-611c-5111-47eab87b7",
      "messageId": "ad13f0d6-bb11-ca23-99aa-312a0b213805"
    },
    "payload": {
      "controls": [
        {
          "enabled": true,
          "name": "PLAY_PAUSE",
          "selected": false,
          "type": "BUTTON"
        },
        {
          "enabled": true,
          "name": "NEXT",
          "selected": false,
          "type": "BUTTON"
        },
        {
          "enabled": true,
          "name": "PREVIOUS",
          "selected": false,
          "type": "BUTTON"
        }
      ],
      "displayType": "list",
      "playableItems": [
        {
          "artImageUrl": "http://musicmeta.musicproviderdomain.com/example/album/662058.jpg",
          "controls": [
            {
              "enabled": true,
              "name": "LIKE_DISLIKE",
              "selected": false,
              "type": "BUTTON"
            }
          ],
          "headerText": "Classic",
          "lyrics": [
            {
              "data": null,
              "format": "PLAIN",
              "url": null
            }
          ],
          "showAdultIcon": false,
          "titleSubText1": "Alice Sara Ott, Symphonie Orchester Des Bayerischen Rundfunks, Esa-Pekka Salonen",
          "titleSubText2": "Wonderland - Edvard Grieg : Piano Concerto, Lyric Pieces",
          "titleText": "Grieg : Piano Concerto In A Minor, Op.16 - 3. Allegro moderato molto e marcato (Live)",
          "token": "eJyr5lIqSSyITy4tKs4vUrJSUE="
        },
        {
          "artImageUrl": "http://musicmeta.musicproviderdomain.com/example/album/202646.jpg",
          "controls": [
            {
              "enabled": true,
              "name": "LIKE_DISLIKE",
              "selected": false,
              "type": "BUTTON"
            }
          ],
          "headerText": "Classic",
          "lyrics": [
            {
              "data": null,
              "format": "PLAIN",
              "url": null
            }
          ],
          "showAdultIcon": false,
          "titleSubText1": "Berliner Philharmoniker, Herbert Von Karajan",
          "titleSubText2": "Mendelssohn : Violin Concerto; A Midsummer Night`s Dream",
          "titleText": "Symphony No.4 In A Op.90 'Italian' - III. Con Moto Moderato",
          "token": "eJyr5lIqSSyITy4tKs4vUrJSUEo2"
        },
        ...
      ],
      "provider": {
        "logoUrl": "https://img.musicproviderdomain.net/logo_180125.png",
        "name": "SampleMusicProvider",
        "smallLogoUrl": "https://img.musicproviderdomain.net/smallLogo_180125.png"
      }
    }
  }
}
```

{% endraw %}

### See also
* [`AudioPlayer.Play`](#Play)
* [`TemplateRuntime.LikeCommandIssued`](#LikeCommandIssued)
* [`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo)
* [`TemplateRuntime.UnlikeCommandIssued`](#UnlikeCommandIssued)

## RequestPlayerInfoIssued event {#RequestPlayerInfoIssued}
Requests CIC for playback metadata such as a playlist, album image, and lyrics to display on the media player. Upon receiving the event, the CIC must send the [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo) directive to the client.


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `token`        | string  | The token of the media content which becomes the starting standard when importing the playback metadata. Make sure to enter the token value provided in the `playableItems[].token` field of the [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo) directive. | Required |
| `range`        | object  | The scope of the playback metadata. If this field is empty, the client will receive a random number of metadata.   | Optional  |
| `range.before` | number  | Requests n number of playback metadata included in the previous playlist from the base media content.  | Optional  |
| `range.after`  | number  | Requests n number of playback metadata included in the next playlist from the existing media content. For example, if the value of `range.after` is set as `5` without specifying the value of `range.before` field, the playback metadata equivalent to a total of six media contents, including the base media content, is received. | Optional  |

### Remarks
* The button on the client device can either be a physical button or a software button like a widget button on a music player.

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "TemplateRuntime",
      "name": "RequestPlayerInfoIssued",
      "messageId": "2fcb6a62-393d-46ad-a5c4-b3db9b640045"
    },
    "payload": {
      "token": "eJyr5lIqSSyITy4tKs4vUrJSUE"
    }
  }
}
```
{% endraw %}

### See also
* [`TemplateRuntime.ExpectRequestPlayerInfo`](#ExpectRequestPlayerInfo)
* [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo)

## UnlikeCommandIssued event {#UnlikeCommandIssued}
Reports to CIC that the user pressed the Unlike button on the client device for a specific media. Upon receiving the event, CIC sends the appropriate directive to the client.


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `token`    | string  | The token of the media content. Make sure to enter the token value provided in the `playableItems[].token` field of the [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo) directive. | Required |

### Remarks
* The button on the client device can either be a physical button or a software button like a widget button on a music player.

### Message example

{% raw %}

```json
{
  "context": [
    {{Alerts.AlertsState}},
    {{AudioPlayer.PlayerState}},
    {{Device.DeviceState}},
    {{Device.Display}},
    {{Clova.Location}},
    {{Clova.SavedPlace}},
    {{Speaker.VolumeState}},
    {{SpeechSynthesizer.SpeechState}}
  ],
  "event": {
    "header": {
      "namespace": "TemplateRuntime",
      "name": "UnlikeCommandIssued",
      "messageId": "2fcb6a62-393d-46ad-a5c4-b3db9b640045"
    },
    "payload": {
      "token": "eJyr5lIqSSyITy4tKs4vUrJSUE"
    }
  }
}
```
{% endraw %}

### See also
* [`TemplateRuntime.LikeCommandIssued`](#LikeCommandIssued)
* [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo)
