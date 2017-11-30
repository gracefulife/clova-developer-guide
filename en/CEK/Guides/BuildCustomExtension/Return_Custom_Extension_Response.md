## Returning custom extension response {#ReturnCustomExtensionResponse}
[After processing a request message](#HandleCustomExtensionRequest), you must return a [response message](/CEK/References/CEK_API.md#CustomExtResponseMessage) back to CEK (HTTPS response). Although details of response can vary depending on the request type, all response messages have a similar structure. Below is a response message returned after a LaunchRequest was processed (user request: "Let's talk in English").

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

The meaning of each field is as follows.

* `version`: The message format version of the current custom extension is v0.1.0.
* `response.outputSpeech`: It is set to speak in English, "Hi, nice to meet you".
* `response.card`: There is no data to display on a client screen. Data format follows [content templates](/CIC/References/Content_Templates.md). You can use this field to return content to display on a client screen.
* `response.shouldEndSession`: The current session does not end
 but continues to receive user input. If this field is set to true, your extension can end the session by itself before receiving a [`SessionEndedRequest`](#HandleSessionEndedRequest).

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
          "lang": "en",
          "value": "Listen to my song."
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
  <p>In addition to simple or complex sentence format, we also support a combined format (SpeechSet) for a client device which does not have a screen or does not provide GUI for displaying detailed information. See <a href="/CEK/References/CEK_API.md#CustomExtResponseMessage">Response message</a> in "Custom extension message" for more details.</p>
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
      "values": {
          "type": "PlainText",
          "lang": "en",
          "value": "How about horror movie?"
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
              "value": "horror, thriller"
            },
            {
              "type": "string",
              "value": "Aaron Eckhart, Carice van Houten, Catalina Sandino Moreno"
            },
            {
              "type": "string",
              "value": ""
            }
          ],
          "imageUrl": {
            "type": "url",
            "value": "http://movie.sample.com/movie_image_incaenate.jpg"
          },
          "linkUrl": {
            "type": "url",
            "value": "http://movie.sample.com/link?title=Incarnate"
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
            "value": "Sample Search Results"
          },
          "referenceUrl": {
            "type": "url",
            "value": "https://search.sample.com/search?query=Incarnate"
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
              "value": "horror"
            },
            {
              "type": "string",
              "value": "Matilda Anna Ingrid Lutz, Alex Roe, Johnny Galecki"
            },
            {
              "type": "string",
              "value": ""
            }
          ],
          "imageUrl": {
            "type": "url",
            "value": "http://movie.sample.com/movie_image_rings.jpg"
          },
          "linkUrl": {
            "type": "url",
            "value": "http://movie.sample.com/link?title=rings"
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
            "value": "Sample Search Results"
          },
          "referenceUrl": {
            "type": "url",
            "value": "https://search.sample.com/search?query=rings"
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
