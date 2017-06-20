## Custom extension 응답 반환하기 {#ReturnCustomExtensionResponse}
[요청 메시지를 처리](#HandleCustomExtensionRequest)하고 나면 다시 CEK로 [응답 메시지](/CEK/References/CEK_Message_Format.md#ResponseMessage)를 돌려줘야 합니다(HTTPS Response). 요청 메시지의 타입에 따라 응답해야 하는 내용이 달라질 수 있지만 응답 메시지의 구조는 크게 차이가 없습니다. 다음은 LaunchRequest 타입 요청("영어 대화하자"라는 사용자 요청)을 처리하고 보낸 응답 메시지입니다.

{% raw %}
```json
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
        "type": "PlainText",
        "text": "You are back. I want to know more about you. Do you go to school?",
        "pause": "0",
        "lang": "en"
    },
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}
```
{% endraw %}

각 필드는 다음과 같은 의미를 가집니다.

* *version* : 현재 사용하는 Custom extension 메시지 포맷의 버전이 v0.1.0입니다.
* *response.outputSpeech* : 사용자에게 영어로 "You are back. I want to know more about you. Do you go to school?"의 문장을 말하도록 설정합니다.
* *response.card* : 클라이언트 화면에 표시할 데이터가 없습니다. [Content Template](/CIC/References/Content_Templates.md) 형태의 데이터이며, 클라이언트 화면에 표시할 콘텐트를 이 필드를 통해 전달할 수 있습니다.
* *response.shouldEndSession* : 현재 세션을 종료하지 않고 계속 사용자의 입력을 받습니다. 만약 이 필드 값이 true이면 *[SessionEndedRequest](#SessionEndedRequest)* 요청을 받기 전에 extension이 주도하여 세션을 종료할 수 있습니다.

<div class="note">
  <p><strong>Note!</strong></p>
  <p><em>sessionAttributes</em> 필드는 확장을 위해 예약해 둔 필드이며, <em>response.directives</em> 필드는 extension이 CEK로 전달하는 지시 메시지입니다. <em>response.directives</em> 필드에서 사용할 지시 메시지는 추후 API를 제공할 예정입니다.</p>
</div>

음성 출력뿐만 아니라 클라이언트 기기의 화면이나 클라이언트 앱 화면에 원하는 데이터를 출력해야 한다면 다음과 같이 *response.card* 필드에 [Content Template](/CIC/References/Content_Templates.md)에 맞춰 표시할 콘텐츠를 입력하면 됩니다.

{% raw %}
```json
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": [
      {
        "type": "PlainText",
        "text": "공포 영화 추천해 드려요.",
        "pause": "0",
        "lang": "ko"
      }
    ],
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



참고로 *response.shouldEndSession*을 이용하면, 부족한 정보를 추가로 확인하기 위해 연속된 대화를 시도할 수 있습니다. 예를 들어, 사용자가 "페퍼로니 피자 주문해줘"라고 했는데 extension 쪽에서 해당 내용을 처리하기 위해 수량과 같은 추가 정보가 필요할 수 있습니다. 그럴 경우 아래와 같이 응답하면 사용자에게 수량과 관련된 추가 정보를 얻을 수 있습니다. 이때 Clova 플랫폼은 대화 엔진을 활용하여 사용자의 이전 요청인 "페퍼로니 피자 주문해줘"와 추가로 얻은 수량 정보를 조합하여 "페퍼로니 피자 2판 주문해줘"와 같은 요청이 입력된 것처럼 정보를 분석하여 전달할 것입니다.

{% raw %}
```json
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": [
      {
        "type": "PlainText",
        "text": "몇 판 주문할까요?",
        "pause": "0",
        "lang": "ko"
      }
    ],
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}
```
{% endraw %}