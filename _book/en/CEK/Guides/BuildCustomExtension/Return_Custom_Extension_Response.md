## Returning custom extension response {#ReturnCustomExtensionResponse}
After [handling a request message](#HandleCustomExtensionRequest) is done, you must return a [response message](/CEK/References/Custom_Extension_Message_Format.md#ResponseMessage) back to CEK (HTTPS response). Although details of response can change depending on the request type, all response messages have a similar structure. Below is a response message returned after a LaunchRequest was processed (user request: "Let's talk in English").

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

The meaning of each field is as follows.

* `version`: The message format version of the current custom extension is v0.1.0.
* `response.outputSpeech`: Set to speak in English, "Hi, nice to meet you".
* `response.card`: There is no data to display on a client screen. Data format follows [content templates](/CIC/References/Content_Templates.md). You can use this field to return content to display on a client screen.
* `response.shouldEndSession`: The current session does not end and continues to receive user input. If this field is set to true, your extension can end the session before receiving a [`SessionEndedRequest`](#SessionEndedRequest).

<div class="note">
  <p><strong>Note!</strong></p>
  <p><code>sessionAttributes</code> is a field reserved for future use. <code>response.directives</code> is a field used in a directive message returned to CEK. The directive message API for the <code>response.directives</code> field will be available in the future.</p>
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

Each `response.outputSpeech` field indicates the following.

* `response.outputSpeech.type`: The speech data is a complex sentence (SpeechList).
* `response.outputSpeech.values[0]`: The speech data is plain text. It is set to speak in Korean, "노래를 불러볼게요".
* `response.outputSpeech.values[1]`: The speech data is a URL. It is set to play a file from the URL in the `value` field.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>In addition to simple or complex sentence format, we also support a combined format (SpeechSet) for a client device which does not have a screen or does not provide GUI for displaying detailed information. See <a href="/CEK/References/Custom_Extension_Message_Format.md#ResponseMessage">Response message</a> in "Custom extension message" for more details.</p>
</div>

To display data on a screen of client device or client app in addition to generating audio output, fill in content in the `response.card` field as follows, using an appropriate [content template](/CIC/References/Content_Templates.md).

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