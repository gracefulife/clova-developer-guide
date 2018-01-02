# 공통 필드
모든 content template는 다음과 같은 공통 필드를 가질 수 있습니다. 공통 필드는 content template 객체의 최상위에 위치하게 됩니다.

| 필드 이름        | 자료형    | 필드 설명                     | 반환 여부 |
|----------------|---------|-----------------------------|---------|
| `actionList[]`     | [ActionObject](/CIC/References/ContentTemplates/Shared_Objects.md#ActionObject) array | UI 터치와 같은 사용자 인터랙션에 대응할 수 있도록 content template을 제공해야합니다. 이때, 이 필드를 이용하여 사용자 인터랙션에 대응할 동작([Action URL scheme](#ActionURLScheme)) 목록을 전달합니다. [CardList](/CIC/References/ContentTemplates/CardList.md) 타입의 content template은 `cardList[]` 필드 하위에 정의될 수 있습니다. | 조건부 반환 |
| `failureMessage` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | UI에 content template를 표시하지 못할 경우 보여줄 메시지 정보를 포함합니다. 예를 들면, 클라이언트가 `meta.version`에 명시된 content template의 버전을 지원하지 않거나 템플릿 정보를 표시하는데 문제가 생길 경우 보여줄 메시지 입니다. | 항상 |
| `meta`             | object | Content template과 관련된 메타 정보를 포함합니다. | 항상 |
| `meta.version`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Content template의 버전 정보를 포함합니다. | 항상 |

## 공통 필드 Example

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
    "value": "경기도 성남시 분당구 정자1동 오늘 미세먼지 지수는 좋음 입니다"
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
공통 필드 중 `actionList` 필드에 다음과 같은 action URL scheme를 사용하여 동작을 정의하고 있습니다.

| Action URL scheme           | 클라이언트가 수행할 동작                                               |
|-----------------------------|------------------------------------------------------------------|
| [clova://app-launch/default-addressbook](#AppLaunchDefaultAddrBook) | 기본 주소록 앱을 실행하는 동작   |
| [clova://app-launch/default-browser](#AppLaunchDefaultBrowser)      | 기본 웹 브라우저를 실행하는 동작 |
| [clova://app-launch/default-camera](#AppLaunchDefaultCamera)        | 기본 카메라 앱을 실행하는 동작   |
| [clova://app-launch/default-email](#AppLaunchDefaultEmail)          | 기본 메일 앱을 실행하는 동작    |
| [clova://app-launch/default-gallery](#AppLaunchDefaultGallery)      | 기본 갤러리 앱을 실행하는 동작   |
| [clova://audio-repeat](#AudioRepeat)                                | 오디오 출력을 수행하는 동작     |
| [clova://device-control](#DeviceControl)                            | 기기 제어를 수행하는 동작       |
| [clova://guide/talking](#GuideTalking)     | 명령 도우미를 제공하는 동작                              |
| [clova://naverSearch](#NaverSearch)        | NAVER 앱에서 특정 키워드를 검색하는 동작                    |
| [clova://naver-maps](#NaverMaps)           | NAVER 지도 앱을 실행하는 동작                            |
| [clova://ttsRepeat](#TTSRepeat)            | Text to speech 발화를 수행하는 동작                     |
| [clova://webview](#Webview)                | WebView로 웹 페이지를 여는 동작                          |

### clova://app-launch/default-addressbook {#AppLaunchDefaultAddrBook}

클라이언트가 기본 주소록 앱을 실행하도록 정의한 스키마입니다. 이 action URL scheme의 예는 다음과 같습니다.

```
clova://app-launch/default-addressbook
```

### clova://app-launch/default-browser {#AppLaunchDefaultBrowser}

클라이언트가 기본 웹 브라우저를 실행하도록 정의한 스키마입니다. 이 action URL scheme의 예는 다음과 같습니다.

```
clova://app-launch/default-browser
```

### clova://app-launch/default-camera {#AppLaunchDefaultCamera}

클라이언트가 기본 카메라 앱을 실행하도록 정의한 스키마입니다. 이 action URL scheme의 예는 다음과 같습니다.

```
clova://app-launch/default-camera
```

### clova://app-launch/default-email {#AppLaunchDefaultEmail}

클라이언트가 기본 메일 앱을 실행하도록 정의한 스키마입니다. 이 action URL scheme의 예는 다음과 같습니다.

```
clova://app-launch/default-email
```

### clova://app-launch/default-gallery {#AppLaunchDefaultGallery}

클라이언트가 기본 갤러리 앱을 실행하도록 정의한 스키마입니다. 이 action URL scheme의 예는 다음과 같습니다.

```
clova://app-launch/default-gallery
```

### clova://audio-repeat {#AudioRepeat}

클라이언트가 오디오 파일 재생을 실행하도록 정의한 스키마입니다.

| 파라미터 이름    | 설명                         | 필수 여부 |
|---------------|-----------------------------|--------|
| url           | 오디오 파일 URL                | 필수 |

이 action URL scheme의 예는 다음과 같습니다.

```
clova://audio-repeat?url=http://target.audioFile.url
```

### clova://device-control {#DeviceControl}

클라이언트가 클라이언트의 특정 기능을 제어하도록 정의한 스키마입니다.

| 파라미터 이름    | 설명                         | 필수 여부 |
|---------------|-----------------------------|--------|
| command       | 제어 명령. <ul><li>BtConnect</li><li>BtDisconnect</li><li>BtStartPairing</li><li>BtStopPairing</li><li>Decrease</li><li>Increase</li><li>LaunchApp</li><li>OpenScreen</li><li>SetValue</li><li>TurnOn</li><li>TurnOff</li></ul>                      | 필수 |
| target        | 제어 대상. <ul><li><code>"airplane"</code>: 비행기 모드</li><li><code>"app"</code>: 앱</li><li><code>"bluetooth"</code>: 블루투스</li><li><code>"cellular"</code>: 모바일 통신</li><li><code>"channel"</code>: TV 채널</li><li><code>"flashlight"</code>: 플래시 조명</li><li><code>"gps"</code>: GPS</li><li><code>"powersave"</code>: 절전 모드</li><li><code>"screenbrightness"</code>: 화면 밝기</li><li><code>"soundmode"</code>: 사운드 모드</li><li><code>"volume"</code>: 스피커 볼륨</li><li><code>"wifi"</code>: 무선랜</li></ul> | 필수 |
| value         | 설정 값. `command` 파라미터가 `setValue`일 때 스피커 볼륨(`"volume"`) 또는 화면 밝기(`"screenbrightness"`)를 설정하거나 TV 채널(`"channel"`)을 설정할 때 지정되는 값입니다. | 선택 |

이 action URL scheme의 예는 다음과 같습니다.

```
clova://device-control?command=SetValue&target=volume&value=5
clova://device-control?command=TurnOn&target=flashlight
```

### clova://guide/talking {#GuideTalking}

클라이언트가 명령 도우미를 제공하도록 정의한 스키마입니다. 이 action URL scheme의 예는 다음과 같습니다.


```
clova://guide/talking
```

### clova://naverSearch {#NaverSearch}

클라이언트가 NAVER 앱을 실행하여 검색 기능을 수행하도록 정의한 스키마입니다.

| 파라미터 이름    | 설명                         | 필수 여부 |
|---------------|-----------------------------|--------|
| url           | NAVER 앱을 통해 열려는 페이지의 URL | 필수 |

이 action URL scheme의 예는 다음과 같습니다.

```
clova://naverSearch?url=http://target.page.url
```

### clova://naver-maps {#NaverMaps}

클라이언트가 NAVER 지도 앱을 실행하여 길찾기 기능을 수행하도록 정의한 스키마입니다.

| 파라미터 이름    | 설명                         | 필수 여부 |
|---------------|-----------------------------|--------|
| url           | NAVER 지도 앱을 통해 열려는 URL   | 필수 |

이 action URL scheme의 예는 다음과 같습니다.

```
clova://naver-maps?url=http://target.map.url
```

### clova://ttsRepeat {#TTSRepeat}

클라이언트가 특정 텍스트를 발화하도록 정의한 스키마입니다.

| 파라미터 이름    | 설명                         | 필수 여부 |
|---------------|-----------------------------|--------|
| lang          | TTS(Text to Speech) 대상 언어. <ul><li><code>"en"</code>: 영어</li><li><code>"ja"</code>: 일본어</li><li><code>"ko"</code>: 한국어</li></ul> | 필수 |
| text          | 발화할 텍스트                   | 선택 |

이 action URL scheme의 예는 다음과 같습니다.

```
clova://ttsRepeat?lang=en&text=hello
```

### clova://webview {#WebView}
클라이언트가 WebView를 이용하여 특정 페이지를 여는 동작을 수행하도록 정의한 스키마입니다.

| 파라미터 이름    | 설명                         | 필수 여부 |
|---------------|-----------------------------|--------|
| url           | 대상 페이지의 URL              | 필수 |
| auth_required | 인증 필요 여부. 이 파라미터가 `true`이면, 대상 페이지를 열 때 인증 API를 사용해야 하며, `false`이거나 명시가 안된 경우 인증이 필요하지 않습니다. | 선택 |

이 action URL scheme의 예는 다음과 같습니다.

```
clova://webview?url=http://target.page.url&auth_required=true
```
