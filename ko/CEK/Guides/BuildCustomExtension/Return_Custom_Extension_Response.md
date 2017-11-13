## Custom extension 응답 반환하기 {#ReturnCustomExtensionResponse}
[요청 메시지를 처리](#HandleCustomExtensionRequest)하고 나면 다시 CEK로 [응답 메시지](/CEK/References/CEK_API.md#CustomExtResponseMessage)를 돌려줘야 합니다(HTTPS Response). 요청 메시지의 타입에 따라 응답해야 하는 내용이 달라질 수 있지만 응답 메시지의 구조는 크게 차이가 없습니다. 다음은 LaunchRequest 타입 요청("영어 대화하자"라는 사용자 요청)을 처리하고 보낸 응답 메시지입니다.

{% raw %}
```json
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values": {
          "type": "PlainText",
          "lang": "en",
          "value": "Hi, nice to meet you"
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}
```
{% endraw %}

각 필드는 다음과 같은 의미를 가집니다.

* `version`: 현재 사용하는 custom extension 메시지 포맷의 버전이 v0.1.0입니다.
* `response.outputSpeech`: 사용자에게 영어로 "Hi, nice to meet you"의 문장을 말하도록 설정합니다.
* `response.card`: 클라이언트 화면에 표시할 데이터가 없습니다. [Content template](/CIC/References/Content_Templates.md) 형태의 데이터이며, 클라이언트 화면에 표시할 콘텐트를 이 필드를 통해 전달할 수 있습니다.
* `response.shouldEndSession`: 현재 세션을 종료하지 않고 계속 사용자의 입력을 받습니다. 만약 이 필드 값이 true이면 [`SessionEndedRequest`](#HandleSessionEndedRequest) 요청을 받기 전에 extension이 주도하여 세션을 종료할 수 있습니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p><code>sessionAttributes</code> 필드는 확장을 위해 예약해 둔 필드이며, <code>response.directives</code> 필드는 extension이 CEK로 전달하는 지시 메시지입니다. <code>response.directives</code> 필드에서 사용할 지시 메시지는 추후 API를 제공할 예정입니다.</p>
</div>

다음과 같이 경우에 따라서 여러 문장을 출력하도록 응답 메시지를 작성할 수도 있고, 인터넷 상에 있는 음성 파일이나 음악 파일을 재생하도록 응답 메시지를 작성할 수도 있습니다.

{% raw %}
```json
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SpeechList",
      "values": [
        {
          "type": "PlainText",
          "lang": "ko",
          "value": "노래를 불러볼게요."
        },
        {
          "type": "URL",
          "lang": "" ,
          "value": "https://tts.com/song.mp3"
        }
      ]
    },
    "card": {},
    "directives": [],
    "shouldEndSession": true
  }
}
```
{% endraw %}

각 `response.outputSpeech` 필드를 설명하면 다음과 같습니다.

* `response.outputSpeech.type`: 복문 타입(SpeechList)의 음성 정보입니다.
* `response.outputSpeech.values[0]`: 일반 텍스트 형태의 음성 정보이며, 한국어로 "노래를 불러볼게요"라고 발화하도록 설정했습니다.
* `response.outputSpeech.values[1]`: URL 형태의 음성 정보이며, `value` 필드에 입력된 URL의 파일을 재생하도록 설정했습니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>단문이나 복문 형태의 음성 정보 외에도 스크린 없는 기기와 같이 상세 내용을 GUI로 표현하기 힘든 클라이언트를 위해 복합 형태(SpeechSet)의 음성 정보도 지원하고 있습니다. 자세한 사항은 custom extension 메시지 포맷의 <a href="/CEK/References/CEK_API.md#CustomExtResponseMessage">응답 메시지</a>를 참조합니다.</p>
</div>

음성 출력뿐만 아니라 클라이언트 기기의 화면이나 클라이언트 앱 화면에 원하는 데이터를 출력해야 한다면 다음과 같이 `response.card` 필드에 [content template](/CIC/References/Content_Templates.md)에 맞춰 표시할 콘텐츠를 채우면 됩니다.

{% raw %}
```json
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values": {
          "type": "PlainText",
          "lang": "ko",
          "value": "공포 영화 추천해 드려요."
      }
    },
    "card": {
      "subType": "",
      "type": "CardList",
      "cardList": [
        {
          "description": [
            {
              "type": "string",
              "value": "공포, 스릴러"
            },
            {
              "type": "string",
              "value": "아론 에크하트, 데이비드 매주즈, 캐리스 밴 허슨, 카타리나 산디노 모레노, 키어 오도넬, 매트 네이블, 존 피루첼로, 엠제이 안소니, 카롤리나 위드라, 마크 스테거, 토마스 아라나, 페트라 스프레처, 마크 헨리, 애슐리 그린 엘리자베스"
            },
            {
              "type": "string",
              "value": ""
            }
          ],
          "imageUrl": {
            "type": "url",
            "value": "http://movie.phinf.naver.net/20170410_12/1491786049305s4W0n_JPEG/movie_image.jpg?type=w640_2"
          },
          "linkUrl": {
            "type": "url",
            "value": "http://movie.naver.com/movie/bi/mi/basic.nhn?code=118965"
          },
          "press": {
            "type": "string",
            "value": ""
          },
          "publishDate": {
            "type": "date",
            "value": ""
          },
          "referenceText": {
            "type": "string",
            "value": "네이버 검색결과"
          },
          "referenceUrl": {
            "type": "url",
            "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=+%ec%98%81%ed%99%94"
          },
          "title": {
            "type": "string",
            "value": "인카네이트"
          },
          "videoUrl": {
            "type": "url",
            "value": ""
          }
        },
        {
          "description": [
            {
              "type": "string",
              "value": "공포"
            },
            {
              "type": "string",
              "value": "마틸다 안나 잉그리드 루츠, 알렉스 로, 자니 갈렉키, 빈센트 도노프리오, 에이미 티가든, 보니 모건, 로라 위긴스, 잭 로어리그, 리지 브로체르"
            },
            {
              "type": "string",
              "value": ""
            }
          ],
          "imageUrl": {
            "type": "url",
            "value": "http://movie.phinf.naver.net/20170317_53/1489741954272MquSW_JPEG/movie_image.jpg?type=w640_2"
          },
          "linkUrl": {
            "type": "url",
            "value": "http://movie.naver.com/movie/bi/mi/basic.nhn?code=137909"
          },
          "press": {
            "type": "string",
            "value": ""
          },
          "publishDate": {
            "type": "date",
            "value": ""
          },
          "referenceText": {
            "type": "string",
            "value": "네이버 검색결과"
          },
          "referenceUrl": {
            "type": "url",
            "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=+%ec%98%81%ed%99%94"
          },
          "title": {
            "type": "string",
            "value": "링스"
          },
          "videoUrl": {
            "type": "url",
            "value": ""
          }
        },
        ...
      ]
    },
    "directives": [],
    "shouldEndSession": true
  }
}
```
{% endraw %}
