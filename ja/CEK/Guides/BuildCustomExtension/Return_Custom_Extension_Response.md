## Custom Extensionレスポンスを返す {#ReturnCustomExtensionResponse}
[リクエストメッセージを処理](#HandleCustomExtensionRequest)すると、CEKに[レスポンスメッセージ](/CEK/References/CEK_API.md#CustomExtResponseMessage)を返す必要があります(HTTPSレスポンス)。リクエストメッセージのタイプによって異なる内容を返すこともありますが、レスポンスメッセージの構造に大差はありません。次は、LaunchRequestタイプのリクエスト(「英会話を始めよう」というユーザーリクエスト)を処理して返したレスポンスメッセージです。

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

各フィールドは、次のような意味を持ちます。

* `version`：使用しているCustom Extensionメッセージフォーマットのバージョンです。現在のバージョンはv0.1.0です。
* `response.outputSpeech`：ユーザーが英語で「Hi, nice to meet you」の文章を話すように設定します。
* `response.card`：クライアントの画面に表示するデータがありません。[コンテンツテンプレート](/CIC/References/Content_Templates.md)形式のデータで、クライアントの画面に表示するコンテンツをこのフィールドで渡すことができます。
* `response.shouldEndSession`：セッションを終了せず、引き続きユーザーの入力を受け付けます。このフィールドの値がtrueの場合、[`SessionEndedRequest`](#HandleSessionEndedRequest)リクエストを受け取る前に、Extensionからセッションを終了できます。

<div class="note">
  <p><strong>メモ</strong></p>
  <p><code>sessionAttributes</code>フィールドは、拡張のために予約されたフィールドです。<code>response.directives</code>フィールドはExtensionがCEKに渡すディレクティブです。<code>response.directives</code>フィールドで使用するディレクティブは、今後APIを提供する予定です。</p>
</div>

次のように、場合によって複数の文章を出力するようにレスポンスメッセージを作成することができます。あるいは、インターネット上のオーディオファイルを再生するようにレスポンスメッセージを作成することもできます。

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
          "lang": "ja",
          "value": "歌を歌ってみます。"
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

各`response.outputSpeech`フィールドの説明は、次のとおりです。

* `response.outputSpeech.type`：複文タイプ(SpeechList)の音声情報です。
* `response.outputSpeech.values[0]`：テキスト形式の音声情報です。日本語で「歌を歌ってみます」と発話するように設定されています。
* `response.outputSpeech.values[1]`：URL形式の音声情報です。`value`フィールドに入力されたURLのファイルを再生するように設定されています。

<div class="note">
  <p><strong>メモ</strong></p>
  <p>単文や複文タイプの音声情報の他にも、画面を持たないデバイスのように、詳しい内容をGUIで表現できないクライアントのために、複合タイプ(SpeechSet)の音声情報もサポートしています。詳細については、Custom Extensionメッセージフォーマットの<a href="/CEK/References/CEK_API.md#CustomExtResponseMessage">レスポンスメッセージ</a>を参照してください。</p>
</div>

音声出力だけでなく、クライアントデバイスの画面やクライアントアプリの画面にデータを出力する必要がある場合、次のように`response.card`フィールドに[コンテンツテンプレート](/CIC/References/Content_Templates.md)に合わせて表示するコンテンツを設定します。

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
          "lang": "ja",
          "value": "ホラー映画をお勧めします。"
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
              "value": "ホラー, スリラー"
            },
            {
              "type": "string",
              "value": "アーロン・エッカート, デヴィッド・マズーズ, カリス・ファン・ハウテン, カタリーナ・サンディーノ・モレーノ, キーア・オドネル, マット・ネイブル, ジョン・プルッチェロ, エムジェイ・アンソニー, カロリーナ・ヴィドラ, マーク・スティガー, トーマス・アラナ, ペトラ・シュプレッヒャー, マーク・ヘンリー, アシュリー・グリーン・エリザベス"
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
            "value": "NAVER検索結果"
          },
          "referenceUrl": {
            "type": "url",
            "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=+%ec%98%81%ed%99%94"
          },
          "title": {
            "type": "string",
            "value": "ドクター・エクソシスト"
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
              "value": "ホラー"
            },
            {
              "type": "string",
              "value": "マチルダ・アンナ・イングリッド・ルッツ, アレックス・ロー, ジョニー・ガレッキ, ヴィンセント・ドノフリオ, エイミー・ティーガーデン, ボニー・モーガン, ローラ・スレイド・ウィッジンズ, ザック・ローリグ, リジー・ブロシュレ"
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
            "value": "NAVER検索結果"
          },
          "referenceUrl": {
            "type": "url",
            "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=+%ec%98%81%ed%99%94"
          },
          "title": {
            "type": "string",
            "value": "ザ・リング／リバース"
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
