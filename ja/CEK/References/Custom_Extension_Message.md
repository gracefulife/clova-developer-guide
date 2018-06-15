## Custom Extensionメッセージ {#CustomExtMessage}
Custom Extensionメッセージは、CEKとCustom Extensionが情報をやり取りする際に使用されるメッセージです。Custom Extensionメッセージには、[リクエストメッセージ](#CustomExtRequestMessage)と[レスポンスメッセージ](#CustomExtResponseMessage)の2種類があります。リクエストメッセージは、[リクエストタイプ](#CustomExtRequestType)によって`LaunchRequest`、`IntentRequest`、`SessionEndedRequest`の3つのタイプがあります。

### リクエストメッセージ {#CustomExtRequestMessage}
CEKは、Clovaが解析したユーザーのリクエストをリクエストメッセージとして、Custom Extensionに渡します(HTTPSリクエスト)。ここでは、リクエストメッセージの構造、各フィールドの説明、リクエストタイプとそれによって異なる`request`フィールドについて説明します。

#### Message structure

{% raw %}
```json
{
  "context": {
    "AudioPlayer": {
      "offsetInMilliseconds": {{number}},
      "playerActivity": {{string}},
      "stream": {{AudioStreamInfoObject}},
      "totalInMilliseconds": {{number}},
    },
    "System": {
      "application": {
        "applicationId": {{string}}
      },
      "device": {
        "deviceId": {{string}},
        "display": {
          "contentLayer": {
            "width": {{number}},
            "height": {{number}}
          },
          "dpi": {{number}},
          "orientation": {{string}},
          "size": {{string}}
        }
      },
      "user": {
        "userId": {{string}},
        "accessToken": {{string}}
      }
    }
  },
  "request": {{object}},
  "session": {
    "new": {{boolean}},
    "sessionAttributes": {{object}},
    "sessionId": {{string}},
    "user": {
      "userId": {{string}},
      "accessToken": {{string}}
    }
  },
  "version": {{string}}
}
```
{% endraw %}

#### Message fields
| フィールド名       | データ型    | フィールドの説明                     | Optional |
|---------------|---------|-----------------------------|:---------:|
| `context`                                  | object  | クライアントのコンテキスト情報を持っているオブジェクト                                |    |
| `context.AudioPlayer`                      | object  | クライアントが現在再生しているか、最後に再生したメディアの情報を持っているオブジェクト | Optional |
| `context.AudioPlayer.offsetInMilliseconds` | number  | 最近再生したメディアの最後の再生ポイント(offset)。単位はミリ秒であり、`playerActivity`の値が"IDLE"の場合、このフィールドは空の場合があります。                                       | Optional |
| `context.AudioPlayer.playerActivity`       | string  | プレイヤーの状態を示す値です。次のような値を持ちます。<ul><li><code>"IDLE"</code>：非アクティブ状態</li><li><code>"PLAYING"</code>：再生中</li><li><code>"PAUSED"</code>：一時停止状態</li><li><code>"STOPPED"</code>：中止状態</li></ul> |    |
| `context.AudioPlayer.stream`               | [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject) | 再生中のオーディオの詳細情報を保存したオブジェクト`playerActivity`の値が`"IDLE"`の場合、このフィールドが空であることがあります。    | Optional |
| `context.AudioPlayer.totalInMilliseconds`  | number  | 最近再生したオーディオの全体の長さ。単位はミリ秒で、`playerActivity`の値が"IDLE"の場合、このフィールドが空であることがあります。                                                                  | Optional |
| `context.System`                           | object  | クライアントシステムのコンテキスト情報を持っているオブジェクト                          |    |
| `context.System.application`               | object  | ユーザーの意図によって実行されるExtensionの情報を持っているオブジェクト       |    |
| `context.System.application.applicationId` | string  | ExtensionのID                                                 |    |
| `context.System.device`                    | object  | クライアントデバイスの情報を持っているオブジェクト                               |    |
| `context.System.device.deviceId`           | string  | クライアントデバイスのID。モデル名とデバイスのシリアル番号を組み合わせた情報など、ユーザーのデバイスを識別できる情報が渡されます。 |    |
| `context.System.device.display`            | object  | クライアントデバイスのディスプレイ情報を持っているオブジェクト                                                 |    |
| `context.System.device.display.contentLayer`        | object | ディスプレイでコンテンツが表示される領域の解像度情報を持つオブジェクト。`context.System.device.display.size`の値が`"none"`の場合、このフィールドは省略されます。  | Optional |
| `context.System.device.display.contentLayer.width`  | number | ディスプレイでコンテンツが表示される領域の幅。ピクセル(px)単位です。             |    |
| `context.System.device.display.contentLayer.height` | number | ディスプレイでコンテンツが表示される領域の高さ。ピクセル(px)単位です。             |    |
| `context.System.device.display.dpi`         | number | ディスプレイ装置のDPI。`context.System.device.display.size`の値が`"none"`の場合、このフィールドは省略されます。          | Optional |
| `context.System.device.display.orientation` | string | ディスプレイ装置の向き。`context.System.device.display.size`の値が`"none"`の場合、このフィールドは省略されます。<ul><li><code>"landscape"</code>：横方向</li><li><code>"portrait"</code>：縦方向</li></ul>                      | Optional |
| `context.System.device.display.size`        | string | ディスプレイ装置の解像度を示す値。あらかじめ指定された値または任意の解像度のサイズを表す値(`"custom"`)が入力されています。しかし、ディスプレイ装置がないことを表す値(`"none"`)が入力されていることもあります。<ul><li><code>"none"</code>：クライアントデバイスにディスプレイ装置がない</li><li><code>"s100"</code>：低解像度(160px X 107px)</li><li><code>"m100"</code>：中解像度(427px X 240px)</li><li><code>"l100"</code>：高解像度(640px X 360px)</li><li><code>"xl100"</code>：超高解像度(xlarge type、899px X 506px)</li><li><code>"custom"</code>：あらかじめ定義された規格ではない解像度。</li></ul><div class="note"><p><strong>メモ</strong></p><p>クライアントデバイスのアスペクト比とDPIに適合した画質のメディアコンテンツを提供する必要があります。</p></div> |    |
| `context.System.user`                      | object  | クライアントデバイスに認証されたのデフォルトユーザーの情報を持っているオブジェクト                 |    |
| `context.System.user.userId`               | string  | デバイスのデフォルトユーザーのClova ID                                    |    |
| `context.System.user.accessToken`          | string  | 特定のサービスのユーザーアカウントのアクセストークン。デバイスのデフォルトユーザーと連携されたユーザーアカウントのアクセストークンが渡されます。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントを連携する](/CEK/Guides/Link_User_Account.md)を参照してください。 |    |
| `request`                                 | object  | 解析されたユーザーの発話情報を持っているオブジェクト。[リクエストタイプ](#CustomExtRequestType)によって、構成されるフィールドが異なります。 |    |
| `session`                                  | object  | セッション情報を持っているオブジェクト。ここでいうセッションとは、ユーザーのリクエストを区分する単位です。     |    |
| `session.new`                              | boolean | リクエストメッセージが新しいセッションに対するものか、それとも既存のセッションに対するものかを区分します。<ul><li>true：新しいセッション</li><li>false：既存のセッション</li></ul>  |    |
| `session.sessionAttributes`                       | object  | ユーザーとのマルチターン対話に必要な情報を保存したオブジェクト。Custom Extensionは、[レスポンスメッセージ](#CustomExtResponseMessage)の`response.sessionAttributes`フィールドを使用して中間情報をCEKに渡します。ユーザーの追加のリクエストを受け付けると、その情報は再びリクエストメッセージの`session.sessionAttributes`フィールドで渡されます。オブジェクトはキー(key)と値(value)のペアで構成され、Custom Extensionを実装する際、任意に定義できます。保存された値がない場合、空のオブジェクトが渡されます。   |    |
| `session.sessionId`                        | string  | セッションID                                                    |    |
| `session.user`                             | object  | 現在のユーザーの情報を持っているオブジェクト                             |    |
| `session.user.userId`                      | string  | 現在のユーザーのClova ID。`context.System.user.userId`の値と異なることがあります。 |    |
| `session.user.accessToken`                 | string  | 特定のサービスのユーザーアカウントのアクセストークン。現在のユーザーと連携されたユーザーアカウントのアクセストークンが渡されます。CEKは、外部サービスの認可サーバーから取得したユーザーアカウントのアクセストークンを渡します。詳細については、[ユーザーアカウントを連携する](/CEK/Guides/Link_User_Account.md)を参照してください。|条件付き |
| `version`                                  | string  | メッセージフォーマットのバージョン(CEKのバージョン)                          |    |

#### Message example
{% raw %}
```json
//例1：LaunchRequestタイプ
{
  "version": "0.1.0",
  "session": {
    "new": true,
    "sessionAttributes": {},
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "application": {
        "applicationId": "com.yourdomain.extension.pizzabot"
      },
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b",
        "display": {
          "size": "l100",
          "orientation": "landscape",
          "dpi": 96,
          "contentLayer": {
            "width": 640,
            "height": 360
          }
        }
      }
    }
  },
  "request": {
    "type": "LaunchRequest"
  }
}

//例2：IntentRequestタイプ
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionAttributes": {},
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "application": {
        "applicationId": "com.yourdomain.extension.pizzabot"
      },
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b",
        "display": {
          "size": "l100",
          "orientation": "landscape",
          "dpi": 96,
          "contentLayer": {
            "width": 640,
            "height": 360
          }
        }
      }
    }
  },
  "request": {
    "type": "IntentRequest",
    "intent": {
      "name": "OrderPizza",
      "slots": {
        "pizzaType": {
          "name": "pizzaType",
          "value": "ペパロニ"
        }
      }
    }
  }
}

//例3：SessionEndedRequestタイプ
{
  "version": "0.1.0",
  "session": {
    "new": false,
    "sessionAttributes": {},
    "sessionId": "a29cfead-c5ba-474d-8745-6c1a6625f0c5",
    "user": {
      "userId": "V0qe",
      "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
    }
  },
  "context": {
    "System": {
      "application": {
        "applicationId": "com.yourdomain.extension.pizzabot"
      },
      "user": {
        "userId": "V0qe",
        "accessToken": "XHapQasdfsdfFsdfasdflQQ7"
      },
      "device": {
        "deviceId": "096e6b27-1717-33e9-b0a7-510a48658a9b",
        "display": {
          "size": "l100",
          "orientation": "landscape",
          "dpi": 96,
          "contentLayer": {
            "width": 640,
            "height": 360
          }
        }
      }
    }
  },
  "request": {
    "type": "SessionEndedRequest"
  }
}
```
{% endraw %}

#### 次の項目も参照してください。
* [Custom Extensionリクエストを処理する](/CEK/Guides/Build_Custom_Extension.md#HandleCustomExtensionRequest)
* [AudioStreamInfoObject](/CIC/References/CICInterface/AudioPlayer.md#AudioStreamInfoObject)

### リクエストタイプ {#CustomExtRequestType}
リクエストメッセージは、次の3つのタイプがあります。リクエストのタイプによって、リクエストメッセージの`request`オブジェクトのフィールドの構成が異なります。
* [`LaunchRequest`](#CustomExtLaunchRequest)
* [`IntentRequest`](#CustomExtIntentRequest)
* [`SessionEndedRequest`](#CustomExtSessionEndedRequest)

#### LaunchRequest {#CustomExtLaunchRequest}
`LaunchRequest`は、ユーザーが特定のExtensionを使用開始したことを知らせるリクエストタイプです。例えば、ユーザーが「英会話始めましょう」と発話した場合など、特定のモードに入ることを宣言した状況です。主に、特定のモードに入るサービスを提供するExtensionがこのタイプのメッセージを受信します。

`LaunchRequest`タイプのメッセージの`request`オブジェクトのフィールドは、次のように構成されます。

{% raw %}
```json
{
  "type": "LaunchRequest"
}
```
{% endraw %}

| フィールド名       | データ型    | フィールドの説明                     | Optional |
|---------------|---------|-----------------------------|:---------:|
| `type`          | string  | リクエストメッセージのタイプ。`"LaunchRequest"`の値に固定されます。 |    |

以下は、LaunchRequestタイプのリクエストメッセージの例です。

#### IntentRequest {#CustomExtIntentRequest}
`IntentRequest`は、解析されたユーザーのリクエストを渡し、その内容を処理するように要求するリクエストタイプです。Extensionの開発者はサービスを開発する際、ユーザーのリクエストをどう受け付けるかについて[対話モデルを定義](/Design/Design_Guideline_For_Extension.md#DefineInteractionModel)する必要があります。対話モデルは、[Clova Developer Center](/DevConsole/ClovaDevConsole_Overview.md)で登録できます。その際、区別されるユーザーのリクエストをインテントという情報形式で定義します。解析されたユーザーの発話情報はインテントに変換され、`intent`フィールドでExtensionに渡されます。

`IntentRequest`タイプのメッセージの`request`オブジェクトのフィールドは、次のように構成されます。

{% raw %}
```json
{
  "type": "IntentRequest",
  "intent": {
    "name": {{string}},
    "slots": {{object}}
  }
}
```
{% endraw %}

| フィールド名       | データ型    | フィールドの説明                     | Optional |
|---------------|---------|-----------------------------|:---------:|
| `type`          | string  | リクエストメッセージのタイプ。`"IntentRequest"`の値に固定されます。                                                                              |    |
| `intent`        | object  | ユーザーのリクエストを解析した情報が保存されたオブジェクト[インテント](/Design/Design_Guideline_For_Extension.md#Intent)                          |    |
| `intent.name`   | string  | インテント名対話モデルに定義した[インテント](/Design/Design_Guideline_For_Extension.md#Intent)をこのフィールドで識別できます。  |    |
| `intent.slots`  | object  | Extensionがインテントを処理する際に要求される情報(スロット)が保存されたオブジェクト。このフィールドは、`intent.name`フィールドに入力された[インテント](/Design/Design_Guideline_For_Extension.md#Intent)によって構成が異なることがあります。 |    |


#### SessionEndedRequest {#CustomExtSessionEndedRequest}
`SessionEndedRequest`タイプは、ユーザーが特定のExtensionの使用を終了したことを示すリクエストです。次の状況でこのメッセージを受信します。
* ユーザーがExtensionの終了をリクエストした場合
* 特定の時間内にユーザーからの入力がない場合(Timeout)
* エラーが発生した場合

<div class="note">
  <p><strong>メモ</strong></p>
  <p><a href="#CustomExtResponseMessage">レスポンスメッセージ</a>の<code>shouldEndSession</code>フィールドを使用して、Extensionから先に終了を宣言した場合には、このメッセージを受信しません。</p>
</div>


`SessionEndedRequest`タイプのメッセージの`request`オブジェクトのフィールドは、次のように構成されます。

{% raw %}
```json
{
  "type": "SessionEndedRequest"
}
```
{% endraw %}

| フィールド名       | データ型    | フィールドの説明                     | Optional |
|---------------|---------|-----------------------------|:---------:|
| `type`          | string  | リクエストメッセージのタイプ。`"SessionEndedRequest"`の値に固定されます。 |    |

### レスポンスメッセージ {#CustomExtResponseMessage}
Extensionは、リクエストメッセージを処理して、レスポンスメッセージを返す必要があります(HTTPSレスポンス)。ここでは、レスポンスメッセージの構造と各フィールドについて説明します。

#### Message structure
{% raw %}
```json
{
  "response": {
    "card": {{object}},
    "directives": [
      {
        "header": {
          "messageId": {{string}},
          "name": {{string}},
          "namespace": {{string}}
        },
        "payload": {{object}}
      }
    ],
    "outputSpeech": {
      "type": {{string}},
      "values": {{SpeechInfoObject|SpeechInfoObject array}},
      "brief": {{SpeechInfoObject}},
      "verbose": {
        "type": {{string}},
        "values": {{SpeechInfoObject|SpeechInfoObject array}},
      }
    },
    "reprompt": {
      "outputSpeech": {
        "type": {{string}},
        "values": {{SpeechInfoObject|SpeechInfoObject array}},
        "brief": {{SpeechInfoObject}},
        "verbose": {
          "type": {{string}},
          "values": {{SpeechInfoObject|SpeechInfoObject array}},
        }
      }
    },
    "shouldEndSession": {{boolean}},
  },
  "sessionAttibutes": {{object}},
  "version": {{string}}
}
```
{% endraw %}

#### Message fields
| フィールド名       | データ型    | フィールドの説明                     | Optional |
|---------------|---------|-----------------------------|:---------:|
| `response`                               | object       | Extensionのレスポンス情報を含むオブジェクト                            |    |
| `response.card`                          | object       | [コンテンツテンプレート](/CIC/References/Content_Templates.md)形式のデータで、クライアントの画面に表示するコンテンツをこのフィールドで渡すことができます。このフィールドにデータがある場合、CICはクライアントに[Clova.RenderTemplate](/CIC/References/CICInterface/Clova.md#RenderTemplate)ディレクティブを渡します。空のオブジェクトの場合、CICはクライアントに[Clova.RenderText](/CIC/References/CICInterface/Clova.md#RenderText)ディレクティブを渡し、`response.outputSpeech.values`フィールドの値を表示するようにします。        |    |
| `response.directives[]`                  | object array | ExtensionがCEKに渡すディレクティブです。`response.directives`フィールドで使用するディレクティブは、今後APIを提供する予定です。 |    |
| `response.directives[].header`           | object       | ディレクティブのヘッダー                                          |    |
| `response.directives[].header.messageId` | string       | メッセージID(UUID)。個別メッセージを区別するために使用される識別子です。   |    |
| `response.directives[].header.name`      | string       | ディレクティブのAPI名                                      |    |
| `response.directives[].header.namespace` | string       | ディレクティブのAPI名前空間                                |    |
| `response.directives[].payload`          | object       | ディレクティブに関する情報を含んでいるオブジェクト。ディレクティブに応じて、payloadオブジェクトの構成とフィールド値を変更できます。         |    |
| `response.outputSpeech`                  | object       | 音声合成する情報を含んでいるオブジェクト。合成された音声はCICを介してクライアントに渡されます。              |    |
| `response.outputSpeech.brief`            | [SpeechInfoObject](#CustomExtSpeechInfoObject) | 出力する音声情報の要約。                    | Optional |
| `response.outputSpeech.type`             | string       | 出力する音声情報のタイプ<ul><li><code>"SimpleSpeech"</code>：単文タイプの音声情報です。最も基本となるタイプで、この値を指定した場合、<code>response.outputSpeech.values</code>フィールドが<a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a>オブジェクトを持っている必要があります。</li><li><code>"SpeechList"</code>：複文タイプの音声情報です。複数の文章を出力する際に使用されます。この値を指定した場合、<code>response.outputSpeech.values</code>フィールドが<a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a>オブジェクト配列を持っている必要があります。</li><li><code>"SpeechSet"</code>：複合タイプの音声情報です。画面を持たないクライアントデバイスに、要約音声情報と詳細音声情報を渡す際に使用されます。この値を指定した場合、<code>response.outputSpeech.values</code>フィールドの代わりに<code>response.outputSpeech.brief</code>と<code>response.outputSpeech.verbose</code>フィールドを持つ必要があります。</li></ul> |    |
| `response.outputSpeech.values[]`           | [SpeechInfoObject](#CustomExtSpeechInfoObject) or [SpeechInfoObject](#CustomExtSpeechInfoObject) array | クライアントデバイスで出力する音声情報を持っているオブジェクトまたはオブジェクト配列 | Optional |
| `response.outputSpeech.verbose`          | object       | 画面を持たないクライアントデバイスに渡す際に使用されます。詳細音声情報を含んでいます。 | Optional |
| `response.outputSpeech.verbose.type`     | string       | 出力する音声情報のタイプ単文と複文タイプの音声情報のみ入力できます。<ul><li><code>"SimpleSpeech"</code>：単文タイプの音声情報です。最も基本的な音声情報を渡す際に使用されます。この値を指定した場合、<code>response.outputSpeech.verbose.values</code>フィールドが<a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a>オブジェクトを持っている必要があります。</li><li><code>"SpeechList"</code>：複文タイプの音声情報です。複数の文章を出力する際に使用されます。この値を指定した場合、<code>response.outputSpeech.verbose.values</code>フィールドが<a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a>オブジェクト配列を持っている必要があります。</li></ul> |    |
| `response.outputSpeech.verbose.values[]`           | [SpeechInfoObject](#CustomExtSpeechInfoObject) or [SpeechInfoObject](#CustomExtSpeechInfoObject) array | クライアントデバイスで出力する詳細音声情報を持っているオブジェクトまたはオブジェクト配列 |    |
| `response.reprompt`                               | obejct       | ユーザーの追加の発話を促す音声情報を含んでいるオブジェクト。`response.reprompt`フィールドを使用すると、ユーザーにマルチターン対話を続けるか尋ねたり、または必須情報を話すように促すことができます。マルチターン対話を行う際、ユーザーが追加の発話をしないまま待っていると、入力待ち時間が過ぎ、マルチターン対話が自動的に終了します。ただし、`response.reprompt`フィールドを使用すると、Clovaは、入力待ち時間が過ぎた後、クライアントが`response.reprompt`フィールドに作成した音声を出力し、再度ユーザーの追加の発話を促すように[`SpeechSynthesizer.Speak`](/CIC/References/CICInterface/SpeechSynthesizer.md#Speak)ディレクティブと[`SpeechRecognizer.ExpectSpeech`](/CIC/References/CICInterface/SpeechRecognizer.md#ExpectSpeech)ディレクティブをクライアントに渡します。<div class="note"><p><strong>メモ</strong></p><p><code>response.reprompt</code>フィールドは、<code>response.shouldEndSession</code>フィールド値を<code>false</code>に入力した場合、有効です。主に単文タイプの音声情報(<code>"SimpleSpeech"</code>)を渡すことをお勧めします。<code>response.reprompt</code>フィールドを使用すると、入力待ち時間を最大1回まで延長できます。</p></div> | Optional |
| `response.reprompt.outputSpeech`                  | object       | 音声に合成する情報を含んでいるオブジェクト。合成された音声はCICを介してクライアントに渡されます。              |    |
| `response.reprompt.outputSpeech.brief`            | [SpeechInfoObject](#CustomExtSpeechInfoObject) | 出力する要約音声情報                    | Optional |
| `response.reprompt.outputSpeech.type`             | string       | 出力する音声情報のタイプ<ul><li>"SimpleSpeech"：単文タイプの音声情報です。最も基本となるタイプであり、この値を指定した場合、<code>response.outputSpeech.values</code>フィールドが<a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a>オブジェクトを持っている必要があります。</li><li><code>"SpeechList"</code>：複文タイプの音声情報です。複数の文章を出力する際に使用されます。この値を指定した場合、<code>response.outputSpeech.values</code>フィールドが<a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a>オブジェクト配列を持っている必要があります。</li><li><code>"SpeechSet"</code>：複合タイプの音声情報です。画面を持たないクライアントデバイスに、要約音声情報と詳細音声情報を渡す際に使用されます。この値を指定した場合、<code>response.outputSpeech.values</code>フィールドの代わりに<code>response.outputSpeech.brief</code>と<code>response.outputSpeech.verbose</code>フィールドを持つ必要があります。</li></ul> |    |
| `response.reprompt.outputSpeech.values[]`           | [SpeechInfoObject](#CustomExtSpeechInfoObject) or [SpeechInfoObject](#CustomExtSpeechInfoObject) array | クライアントデバイスで出力する音声情報を持っているオブジェクトまたはオブジェクト配列 | Optional |
| `response.reprompt.outputSpeech.verbose`          | object       | 画面を持たないクライアントデバイスに音声を渡す際に使用されます。詳細音声情報を含んでいます。 | Optional |
| `response.reprompt.outputSpeech.verbose.type`     | string       | 出力する音声情報のタイプ単文と複文タイプの音声情報のみ入力できます。<ul><li><code>"SimpleSpeech"</code>：単文タイプの音声情報です。最も基本的な音声情報を渡す際に使用されます。この値を指定した場合、<code>response.outputSpeech.verbose.values</code>フィールドが<a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a>オブジェクトを持っている必要があります。</li><li><code>"SpeechList"</code>：複文タイプの音声情報です。複数の文章を出力する際に使用されます。この値を指定した場合、<code>response.outputSpeech.verbose.values</code>フィールドが<a href="#CustomExtSpeechInfoObject"><code>SpeechInfoObject</code></a>オブジェクト配列を持っている必要があります。</li></ul> |    |
| `response.reprompt.outputSpeech.verbose.values[]`           | [SpeechInfoObject](#CustomExtSpeechInfoObject) or [SpeechInfoObject](#CustomExtSpeechInfoObject) array | クライアントデバイスで出力する詳細音声情報を持っているオブジェクトまたはオブジェクト配列 |    |
| `response.shouldEndSession`              | boolean      | セッション終了のフラグ。クライアントに起動中のExtensionの使用が終了したことを示すフィールドです。[`SessionEndedRequest`](#CustomExtSessionEndedRequest)タイプのリクエストメッセージを受け取る前に、Extensionから先に使用終了を示す際に利用できます。<ul><li>true：使用を終了する</li><li>false：引き続き使用する。ユーザーとマルチターン対話を行います。</li></ul> |    |
| `sessionAttributes`                      | object       | ユーザーとのマルチターン対話に必要な情報を保存するために使用されるオブジェクト。Custom Extensionは、`sessionAttributes`フィールドを使用して会話の途中までの情報をCEKに渡します。ユーザーの追加のリクエストを受け付けると、その情報は再び[リクエストメッセージ](#CustomExtRequestMessage)の`session.sessionAttributes`フィールドで渡されます。`sessionAttributes`オブジェクトは、キー(key)と値(value)のペアで構成され、Custom Extensionを実装する際に任意で定義できます。保存する値がない場合、空のオブジェクトを入力します。 |    |
| `version`                                | string       | メッセージフォーマットのバージョン(CEKのバージョン)                        |    |

<div class="note">
  <p><strong>メモ</strong></p>
  <p><code>response.directives</code>フィールドでExtensionに任意のディレクティブを渡したいなどのご要望については、事前に提携担当者までご連絡下さい。</p>
</div>

#### SpeechInfoObject {#CustomExtSpeechInfoObject}
SpeechInfoObjectオブジェクトはレスポンスメッセージの`response.outputSpeech`で再使用されるオブジェクトです。ユーザーに出力する音声情報の最も小さな単位である単文レベルの発話情報です。このオブジェクトは、次のフィールドを持ちます。

| フィールド名        | データ型         | 説明                                                                | Optional |
|----------------|--------------|--------------------------------------------------------------------|:-----:|
| `lang`           | string       | 音声を合成する際に使用する言語のコード。現在、次の値を持ちます。<ul><li><code>"en"</code>：英語</li><li><code>"ja"</code>：日本語</li><li><code>"ko"</code>：韓国語</li><li><code>""</code>：<code>type</code>フィールドの値が<code>"URL"</code>の場合、このフィールドは空の文字列(empty string)を持ちます。</li></ul>         |    |
| `type`           | string       | 再生する音声のタイプ。このフィールドの値によって、`value`フィールドの値の形式が異なります。現在、次の値を持ちます。<ul><li><code>"PlainText"</code>：テキスト</li><li><code>"URL"</code>：音声および音楽を再生できるファイルのURI</li></ul>            |    |
| `value`          | string       | 音声を合成する内容または音声ファイルのURI                                    |    |

#### Message example
{% raw %}
```json
//例1：単文タイプ(SimpleSpeech)の音声情報を返す-テキスト
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

//例2：単文タイプ(SimpleSpeech)の音声情報を返す-テキスト、URLを使用
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

//例3：複合タイプ(SpeechSet)の音声情報を返す-要約・詳細音声情報
{
  "version": "0.1.0",
  "sessionAttributes": {},
  "response": {
    "outputSpeech": {
      "type": "SpeechSet",
      "brief": {
        "type": "PlainText",
        "lang": "ja",
        "value": "天気予報です。"
      },
      "verbose": {
        "type": "SpeechList",
        "values": [
          {
              "type": "PlainText",
              "lang": "ja",
              "value": "週末まで全国に梅雨…猛暑和らぐ。"
          },
          {
              "type": "PlainText",
              "lang": "ja",
              "value": "明日全国的に梅雨…ところによって局地的に激しい雨に注意。"
          }
          ...
        ]
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": true
  }
}

//例4：マルチターン対話で、対話の中間情報を保存する-sessionAttributesを使用
{
  "version": "0.1.0",
  "sessionAttributes": {
    "RequestedIntent": "OrderPizza",
    "pizzaType": "ペパロニピザ"
  },
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values": {
          "type": "PlainText",
          "lang": "ja",
          "value": "何枚注文しますか?"
      }
    },
    "card": {},
    "directives": [],
    "shouldEndSession": false
  }
}

//例5：マルチターン対話でユーザーの追加の発話を促す-repromptを使用
{
  "version": "0.1.0",
  "sessionAttributes": {
    "RequestedIntent": "OrderPizza",
    "pizzaType": "ペパロニピザ"
  },
  "response": {
    "outputSpeech": {
      "type": "SimpleSpeech",
      "values": {
          "type": "PlainText",
          "lang": "ja",
          "value": "何枚注文しますか?"
      }
    },
    "card": {},
    "reprompt" : {
      "outputSpeech" : {
        "type" : "SimpleSpeech",
        "values" : {
          "type" : "PlainText",
          "lang" : "ja",
          "value" : "お言葉がなければ、注文をキャンセルしてよろしいですか?"
        }
      }
    },
    "shouldEndSession": false
  }
}
```
{% endraw %}

#### 次の項目も参照してください。
* [Custom Extensionレスポンスを返す](/CEK/Guides/Build_Custom_Extension.md#ReturnCustomExtensionResponse)
* [コンテンツテンプレート](/CIC/References/Content_Templates.md)
