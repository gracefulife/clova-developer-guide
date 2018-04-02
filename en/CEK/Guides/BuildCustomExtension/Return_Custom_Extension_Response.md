## Returning a custom extension response {#ReturnCustomExtensionResponse}
After [handling the request message](#HandleCustomExtensionRequest), you must return the HTTPS [response message](/CEK/References/CEK_API.md#CustomExtResponseMessage) to the CEK again. The details of the response may vary depending on the type of request message, but the structure of the response message does not vary much. Below is a response message sent after handling a LaunchRequest type request, where a user says "Let’s talk in English."

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

The fields represent the following information:

* `version`: The current version of the custom extension message format is v0.1.0.
* `response.outputSpeech`: The response "Hi, nice to meet you" is set to be said to the user in English.
* `response.card`: There is no data to display on the client screen. The data is in the [content template](/CIC/References/Content_Templates.md) format and can be displayed on the client screen via this field.
* `response.shouldEndSession`: The current session does not end and continuously receives user input. If the field value is set to true, the extension can end the session before receiving the [`SessionEndedRequest`](#HandleSessionEndedRequest) request.

<div class="note">
  <p><strong>Note!</strong></p>
  The <p><code>sessionAttributes</code> field is reserved for future use and the <code>response.directives</code> field is a directive message returned by the extension to CEK. The directive message API for the <code>response.directives</code> field will be provided in the future.</p>
</div>

The response message can be written to output multiple sentences based on the circumstances or to play audio or music files on the Internet as shown below.

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
          "value": "I will sing a song."
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

The `response.outputSpeech` fields represent the following information:

* `response.outputSpeech.type`: A complex type (SpeechList) of audio data.
* `response.outputSpeech.values[0]`: A regular text type of audio data. It has been set to say "I will sing a song" in Korean.
* `response.outputSpeech.values[1]`: A URL type of audio data. It has been set to play a file from the URL entered in the `value` field.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>In addition to simple or complex sentence type of audio data, we support a combined format (SpeechSet) for client devices with limitations for expressing detailed GUIs, such as screenless devices. For more information, see <a href="/CEK/References/CEK_API.md#CustomExtResponseMessage">Response message</a> in the custom extension message format.</p>
</div>

To display data on the screen of a client device or client app in addition to outputting audio, fill in the content in the `response.card` field in accordance with the [content template](/CIC/References/Content_Templates.md).

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
          "value": "I will recommend a horror movie."
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
              "value": "Horror, thriller"
            },
            {
              "type": "string",
              "value": "Aaron Eckhart, David Mazouz, Carice van Houten, Catalina Sandino Moreno, Keir O'Donnell, Matt Nable, John Pirruccello, Emjay Anthony, Karolina Wydra, Mark Steger, Tomas Arana, Petra Sprecher, Mark Henry, Ashley Green Elizabeth"
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
            "value": "NAVER search result"
          },
          "referenceUrl": {
            "type": "url",
            "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=+%ec%98%81%ed%99%94"
          },
          "title": {
            "type": "string",
            "value": "Incarnate"
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
              "value": "Horror"
            },
            {
              "type": "string",
              "value": "Matilda Anna Ingrid Lutz, Alex Roe, Johnny Galecki, Vincent D'Onofrio, Aimee Teegarden, Bonnie Morgan, Laura Wiggins, Zach Roerig, Lizzie Brochere"
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
            "value": "NAVER search result"
          },
          "referenceUrl": {
            "type": "url",
            "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=+%ec%98%81%ed%99%94"
          },
          "title": {
            "type": "string",
            "value": "Rings"
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

