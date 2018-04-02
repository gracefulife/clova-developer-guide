# TemplateRuntime

TemplateRuntime 인터페이스는 클라이언트나 CIC가 미디어 플레이어에 표시할 재생 메타 정보를 요청하거나 전달할 때 사용됩니다. 실제 오디오 스트림 재생에 필요한 정보와 관련된 작업을 수행할 때는 [`AudioPlayer`] 인터페이스를 사용하고 재생 목록, 앨범 이미지, 가사와 같은 재생 메타 정보와 관련된 작업을 수행할 때는 `TemplateRuntime` 인터페이스를 사용해야 합니다. 이를 통해 자신 뿐만 아니라 다른 클라이언트 기기의 재생 메타 정보를 조회하고 사용자에게 제공할 수도 있습니다.

| 메시지 이름         | 메시지 타입  | 메시지 설명                                   |
|------------------|-----------|---------------------------------------------|
| [`ExpectRequestPlayerInfo`](#ExpectRequestPlayerInfo)  | Directive | 클라이언트에게 재생 메타 정보를 요청하도록 지시합니다. 클라이언트는 이 지시 메시지를 받으면 [`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo) 이벤트 메시지를 CIC로 전송해야 합니다. |
| [`LikeCommandIssued`](#LikeCommandIssued)              | Event     | 사용자가 클라이언트 기기에서 미디어 플레이어에서 특정 미디어에 대해 좋아요 버튼(Like)을 누른 경우 클라이언트는 이 이벤트 메시지를 CIC에게 전송해야 합니다. |
| [`RenderPlayerInfo`](#RenderPlayerInfo)                | Directive | CIC가 클라이언트에게 미디어 플레이어에 표시할 재생 목록, 앨범 이미지, 가사와 같은 재생 메타 정보를 전달하고 이를 표시하도록 지시합니다. |
| [`RequestPlayerInfo`](#RequestPlayerInfo)              | Event     | 클라이언트가 미디어 플레이어에 표시할 재생 목록, 앨범 이미지, 가사와 같은 재생 메타 정보를 CIC에게 요청합니다. |
| [`UnlikeCommandIssued`](#UnlikeCommandIssued)          | Event     | 사용자가 클라이언트 기기에서 미디어 플레이어에서 특정 미디어에 대해 좋아요 취소 버튼(Unlike)을 누른 경우 클라이언트는 이 이벤트 메시지를 CIC에게 전송해야 합니다. |

## ExpectRequestPlayerInfo directive {#ExpectRequestPlayerInfo}

클라이언트에게 재생 목록, 앨범 이미지, 가사와 같은 재생 메타 정보를 요청하도록 지시합니다. 클라이언트는 이 지시 메시지를 받으면 [`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo) 이벤트 메시지를 CIC로 전송해야 합니다.

### Payload fields

없음

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
사용자가 클라이언트 기기에서 미디어 플레이어에서 특정 미디어에 대해 좋아요 버튼(Like)을 누른 경우 클라이언트는 이 이벤트 메시지를 CIC에게 전송해야 합니다. 이 이벤트 메시지를 받은 CIC는 상황에 맞는 지시 메시지를 클라이언트에게 전송합니다.


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`    | string  | 미디어 콘텐츠의 token. [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo) 지시 메시지의 `playableItems[].token` 필드로 제공된 token 값이 입력되어야 합니다. | 필수 |

### Remarks
* 클라이언트 기기의 버튼은 물리적인 하드웨어 방식의 버튼일 수도 있고 음악 플레이어 위젯 버튼과 같은 소프트웨어 방식의 버튼일 수도 있습니다.

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

CIC가 클라이언트에게 미디어 플레이어에 표시할 재생 목록, 앨범 이미지, 가사와 같은 재생 메타 정보를 전달하고 이를 표시하도록 지시합니다. 사용자가 음악 재생을 요청한 경우 클라이언트는 [`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play) 지시 메시지를 받아 미디어를 재생하게 됩니다. 이때, 디스플레이 장치가 있는 클라이언트라면 필요에 따라 미디어 플레이어에 재생 관련 정보를 표현해야 할 수 있습니다. 이때, [`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo) 이벤트 메시지를 통해 재생 메타 정보를 CIC에 요청할 수 있으며, `TemplateRuntime.RenderPlayerInfo` 지시 메시지를 수신할 수 있습니다. `TemplateRuntime.RenderPlayerInfo` 지시 메시지는 현재 재생해야 하는 미디어 콘텐츠와 추후 재생해야 하는 미디어 콘텐츠의 재생 메타 정보를 담고 있습니다. 클라이언트는 `TemplateRuntime.RenderPlayerInfo` 지시 메시지의 재생 메타 정보를 사용자에게 제공하므로써 현재 재생 미디어의 메타 정보 및 재생 목록을 표시할 수 있습니다. 뿐만 아니라 사용자가 목록에 있는 특정 미디어를 재생하도록 요청하거나 좋아요([`TemplateRuntime.LikeCommandIssued`](#LikeCommandIssued)), 좋아요 취소([`TemplateRuntime.UnlikeCommandIssued`](#UnlikeCommandIssued))와 같은 동작을 수행할 때 이를 처리할 수 있는 기반 데이터(`token`)를 제공합니다.

### Payload fields
| 필드 이름       | 자료형    | 필드 설명                     | 포함 여부 |
|---------------|---------|-----------------------------|:---------:|
| `displayType`               | string | 미디어 콘텐츠 표시 형태.<ul><li><code>"list"</code>: 목록 표시 형태</li><li><code>"single"</code>: 단일 항목 표시 형태</li></ul>       | 항상 |
| `controls[]`                | object array | 클라이언트가 미디어 플레이어에서 반드시 표시해야 버튼의 정보를 담고 있는 객체 배열입니다.             | 항상 |
| `controls[].enabled`        | boolean      | `controls[].name`에 명시된 버튼이 미디어 플레이어에서 활성화되어야 하는지 나타냅니다.<ul><li><code>true</code>: 활성화</li><li><code>false</code>: 비활성화</li></ul>  | 항상  |
| `controls[].name`           | string       | 버튼 이름. 다음과 같은 값이 포함될 수 있습니다.<ul><li><code>"NEXT"</code>: 다음 버튼</li><li><code>"PLAY_PAUSE"</code>: 재생/일시 정지 버튼</li><li><code>"PREVIOUS"</code>: 이전 버튼</li></ul>  | 항상  |
| `controls[].selected`       | boolean      | 미디어 콘텐츠가 선택된 상태 여부. 이 값은 선호 항목의 개념이 들어간 것을 표현할 때 사용될 수 있습니다. 이 값이 `true`로 선택되었다면 사용자가 선호 항목으로 등록해둔 콘텐츠이기 때문에 미디어 플레이어에서 관련된 UI에 표현해야 합니다. <ul><li><code>true</code>: 선택됨</li><li><code>false</code>: 선택 안됨</li></ul> | 항상  |
| `controls[].type`           | string       | 버튼의 타입. 현재는 `"BUTTON"` 값만 사용됩니다.  | 항상 |
| `playableItems[]`           | object array | 재생할 수 있는 미디어 콘텐츠 목록의 정보를 담고 있는 객체 배열입니다. 이 필드는 빈 배열일 수 있습니다.  | 항상 |
| `playableItems[].artImageUrl`  | string    | 미디어 콘텐츠 관련 이미지의 URL. 앨범 자켓 이미지나 관련 아이콘 등의 이미지가 위치한 URL입니다.      | 조건부 |
| `playableItems[].controls[]`                | object array  | 특정 미디어 콘텐츠를 재생할 때 반드시 표시해야 하는 버튼의 정보를 담고 있는 객체 배열입니다. 이 객체 배열을 생략될 수 있습니다.  | 조건부 |
| `playableItems[].controls[].enabled`        | boolean      | `playableItems[].controls[].name`에 명시된 버튼이 미디어 플레이어에서 활성화되어야 하는지 나타냅니다.<ul><li><code>true</code>: 활성화</li><li><code>false</code>: 비활성화</li></ul>  | 항상  |
| `playableItems[].controls[].name`           | string       | 버튼 이름. 다음과 같은 값이 포함될 수 있습니다.<ul><li><code>"NEXT"</code>: 다음 버튼</li><li><code>"PLAY_PAUSE"</code>: 재생/일시 정지 버튼</li><li><code>"PREVIOUS"</code>: 이전 버튼</li></ul>  | 항상  |
| `playableItems[].controls[].selected`       | boolean      | 미디어 콘텐츠가 선택된 상태 여부. 이 값은 선호 항목의 개념이 들어간 것을 표현할 때 사용될 수 있습니다. 이 값이 `true`로 선택되었다면 사용자가 선호 항목으로 등록해둔 콘텐츠이기 때문에 미디어 플레이어에서 관련된 UI에 표현해야 합니다. <ul><li><code>true</code>: 선택됨</li><li><code>false</code>: 선택 안됨</li></ul> | 항상  |
| `playableItems[].controls[].type`           | string       | 버튼의 타입. 현재는 `"BUTTON"` 값만 사용됩니다.  | 항상 |
| `playableItems[].headerText`       | string        | 주로 현재 재생 목록의 제목을 표현하는 텍스트 필드                                                | 조건부  |
| `playableItems[].lyrics[]`         | object array  | 가사 정보를 담고 있는 객체 배열.                                                            | 조건부  |
| `playableItems[].lyrics[].data`    | string        | 가사 데이터. 이 필드 또는 `playableItems[].lyrics[].url` 필드 중 하나는 존재합니다.              | 조건부  |
| `playableItems[].lyrics[].format`  | string        | 가사 데이터의 포맷.<ul><li><code>"LRC"</code>: <a href="https://en.wikipedia.org/wiki/LRC_(file_format)" target="_blank">LRC 포맷</a></li><li><code>"PLAIN"</code>: 일반 텍스트 형식</li></ul>  | 항상  |
| `playableItems[].lyrics[].url`     | string        | 가사 데이터의 URL. 이 필드 또는 `playableItems[].lyrics[].data` 필드 중 하나는 존재합니다.        | 조건부  |
| `playableItems[].showAdultIcon`    | boolean       | 성인용 콘텐츠를 나타내는 아이콘의 표시 여부.<ul><li><code>true</code>: 표시해야 함.</li><li><code>false</code>: 표시 안해야 함.</li></ul>   | 항상  |
| `playableItems[].titleSubText1`    | string        | 주로 가수 이름을 표현하는 텍스트 필드                                                          | 항상 |
| `playableItems[].titleSubText2`    | string        | 주로 앨범 이름을 표현하는 보조 텍스트 필드                                                      | 조건부 |
| `playableItems[].titleText`        | string        | 현재 음악의 제목을 표현하는 텍스트 필드                                                         | 항상  |
| `playableItems[].token`            | string        | 미디어 콘텐츠의 token                                                                     | 항상 |
| `provider`                         | object        | 미디어 콘텐츠 제공자의 정보가 담긴 객체                                                         | 조건부 |
| `provider.logoUrl`                 | string        | 미디어 콘텐츠 제공자 로고 이미지의 URL                                                         | 조건부 |
| `provider.name`                    | string        | 미디어 콘텐츠 제공자의 이름                                                                   | 항상  |
| `provider.smallLogoUrl`            | string        | 크기가 작은 미디어 콘텐츠 제공자 로고 이미지의 URL                                                | 조건부 |

### Message example
{% raw %}

```json
// 바로 재생 가능한 오디오 스트림 URL 정보가 담긴 예제
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
클라이언트가 미디어 플레이어에 표시할 재생 목록, 앨범 이미지, 가사와 같은 재생 메타 정보를 CIC에게 요청합니다. 이 이벤트 메시지를 CIC에게 전송하면 CIC는 [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo) 지시 메시지를 클라이언트에게 전송합니다.


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`        | string  | 재생 메타 정보를 가져올 때 시작 기준이 되는 미디어 콘텐츠의 token. [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo) 지시 메시지의 `playableItems[].token` 필드로 제공된 token 값이 입력되어야 합니다. | 필수 |
| `range`        | object  | 재생 메타 정보의 범위를 지정하는 객체. 이 필드가 사용되지 않으면 클라이언트는 임의의 개수만큼 메타 정보를 수신하게 됩니다.   | 선택  |
| `range.before` | number  | 기준 미디어 콘텐츠로부터 n개만큼 이전 재생 목록에 포함되는 재생 메타 정보를 요청합니다.  | 선택  |
| `range.after`  | number  | 기준 미디어 콘텐츠로부터 n개만큼 다음 재생 목록에 포함되는 재생 메타 정보를 요청합니다. 예를 들어, `range.before` 필드의 값을 지정하지 않고 `range.after`의 값을 `5`로 설정하면 기준 미디어 콘텐츠를 포함한 총 6개의 미디어 콘텐츠에 해당하는 재생 메타 정보를 수신하게 됩니다. | 선택  |

### Remarks
* 클라이언트 기기의 버튼은 물리적인 하드웨어 방식의 버튼일 수도 있고 음악 플레이어 위젯 버튼과 같은 소프트웨어 방식의 버튼일 수도 있습니다.

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
사용자가 클라이언트 기기에서 미디어 플레이어에서 특정 미디어에 대해 좋아요 취소 버튼(Unlike)을 누른 경우 클라이언트는 이 이벤트 메시지를 CIC에게 전송해야 합니다. 이 이벤트 메시지를 받은 CIC는 상황에 맞는 지시 메시지를 클라이언트에게 전송합니다.


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|:---------:|
| `token`    | string  | 미디어 콘텐츠의 token. [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo) 지시 메시지의 `playableItems[].token` 필드로 제공된 token 값이 입력되어야 합니다. | 필수 |

### Remarks
* 클라이언트 기기의 버튼은 물리적인 하드웨어 방식의 버튼일 수도 있고 음악 플레이어 위젯 버튼과 같은 소프트웨어 방식의 버튼일 수도 있습니다.

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
