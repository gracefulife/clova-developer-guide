## Returning custom extension response {#ReturnCustomExtensionResponse}
After [handling a request message](#HandleCustomExtensionRequest) is done, you must return a [response message](/CEK/References/Custom_Extension_Message_Format.md#ResponseMessage) back to CEK (HTTPS response). Although details of response can vary depending on the request type, response messages have a similar structure overall. Below is a response message returned after a LaunchRequest was processed (user request: "Let's have a conversation in English").

{% raw %}
```json
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values" : {
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

Each field indicates as follows.

* *version*: The message format version of current custom extension is v0.1.0.
* *response.outputSpeech*: Speaks to a user in English, "Hi, nice to meet you".
* *response.card*: There is no data to display on client screen. Data format follows [Content Template](/CIC/References/Content_Templates.md). You can use this field to return content you want to display on client screen.
* *response.shouldEndSession*: Does not end the current session and continues to receive user input. If this field is set to true, you can end the session before receiving *[SessionEndedRequest](#SessionEndedRequest)*.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>The <em>sessionAttributes</em> field is reserved for future use. The <em>response.directives</em> field contains a directive message which your extension sends to CEK. API will be provided in the future for the directive messages that will be included in the <em>response.directives</em> field.</p>
</div>

As shown below, you can write a response message for speaking several sentences of synthesized speech (text-to-speech) or playing an audio or music file from internet.

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

Each field in *response.outputSpeech* indicates the following.

* *response.outputSpeech.type*: Speech output data in SpeechList type.
* *response.outputSpeech.values[0]*: Speech output data in plain text type. It sets to speak in Korean, "노래를 불러볼게요".
* *response.outputSpeech.values[1]*: Speech output data in URL type. It sets to play a file from the URL in *value* field.

<div class="note">
  <p><strong>Note!</strong></p>
    <p>In addition to speech output in simple or complex sentence format, we also support combined format (SpeechSet) for a client device which does not have a screen or does not provide GUI for displaying detailed information. For more details, see <a href="/CEK/References/Custom_Extension_Message_Format.md#ResponseMessage">Response message</a> in "Custom extension message format".</p>
</div>

If you want to display data on a screen of client device or app besides audio output of synthesized speech, fill in content in *response.card* field as follows using [Content Template](/CIC/References/Content_Templates.md).

{% raw %}
```json
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values" : {
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



When *response.shouldEndSession* is set to false, your extension can try to continue conversation with the user when it has to obtain more information. For example, if a user requested, "Order pepperoni pizza", the extension may require additional information such as how many pizzas the user wants to order. In this case, it can obtain information for the quantity from the user by responding as follows. The dialog engine in the Clova platform combines the user's original request, "Order pepperoni pizza" and required quantity of pizza additionally obtained from the user and returns analysis details, "order two pepperoni pizzas".

{% raw %}
```json
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values" : {
          "type": "PlainText",
          "lang": "ko",
          "value": "몇 판 주문할까요?"
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}
```
{% endraw %}