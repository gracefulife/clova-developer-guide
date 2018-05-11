# TemplateRuntime

TemplateRuntimeインターフェースは、クライアントまたはCICがメディアプレーヤーに表示するメタデータをリクエストしたり、送信したりする際に使用します。実際にオーディオストリームの再生に必要なデータに関連する作業を処理する際には[`AudioPlayer`](/CIC/References/CICInterface/AudioPlayer.md)インターフェースを、再生リストやアルバムの画像、歌詞のようなメタデータに関連する作業を処理する際には、`TemplateRuntime`インターフェースを使用します。該当するクライアントのみでなく、他のクライアントデバイスの再生メタデータを照会し、ユーザーに提供することもできます。

| メッセージ         | タイプ  | 説明                                   |
|------------------|-----------|---------------------------------------------|
| [`ExpectRequestPlayerInfo`](#ExpectRequestPlayerInfo)  | ディレクティブ | クライアントに、再生メタデータをリクエストするように指示します。クライアントはこのディレクティブを受信すると、[`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo)イベントをCICに送信する必要があります。 |
| [`LikeCommandIssued`](#LikeCommandIssued)              | イベント     | ユーザーがクライアントのメディアプレーヤーで、特定のメディアに対して「いいね」ボタンを押した場合、クライアントはこのイベントをCICに送信する必要があります。 |
| [`RenderPlayerInfo`](#RenderPlayerInfo)                | ディレクティブ | CICから、メディアプレーヤーに表示する再生リスト、アルバムの画像、歌詞のような再生メタデータをクライアントに送信し、表示するように指示します。 |
| [`RequestPlayerInfo`](#RequestPlayerInfo)              | イベント     | クライアントから、メディアプレーヤーに表示する再生リスト、アルバムの画像、歌詞のような再生メタデータをCICにリクエストします。 |
| [`UnlikeCommandIssued`](#UnlikeCommandIssued)          | イベント     | ユーザーがクライアントのメディアプレーヤーで、特定のメディアに対して「いいね」を取り消すボタン(Unlike)を押した場合、クライアントはこのイベントをCICに送信する必要があります。 |

## ExpectRequestPlayerInfoディレクティブ {#ExpectRequestPlayerInfo}

クライアントに再生リスト、アルバムの画像、歌詞のような再生メタデータをリクエストするように指示します。クライアントはこのディレクティブを受信すると、[`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo)イベントをCICに送信する必要があります。

### Payload fields

なし

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

### 次の項目も参照してください。
* [`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo)

## LikeCommandIssuedイベント {#LikeCommandIssued}
ユーザーがクライアントのメディアプレーヤーで、特定のメディアに対して「いいね」ボタンを押した場合、クライアントはこのイベントをCICに送信する必要があります。CICはこのイベントを受信すると、適切なディレクティブをクライアントに送信します。


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`    | string  | メディアコンテンツのトークン。[`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo)ディレクティブの`playableItems[].token`フィールドで提供されたトークンが入力される必要があります。 | 必須 |

### 備考
* クライアントデバイスのボタンは、ハードウェア方式の物理ボタンの場合もあり、オーディオプレーヤーウィジェットのボタンのようなソフトウェア方式のボタンの場合もあります。

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

### 次の項目も参照してください。
* [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo)
* [`TemplateRuntime.UnlikeCommandIssued`](#UnlikeCommandIssued)

## RenderPlayerInfoディレクティブ {#RenderPlayerInfo}

CICから、メディアプレーヤーに表示する再生リスト、アルバムの画像、歌詞のような再生メタデータをクライアントに送信し、表示するように指示します。ユーザーからオーディオの再生をリクエストされたとき、クライアントは[`AudioPlayer.Play`](/CIC/References/CICInterface/AudioPlayer.md#Play)を受信してメディアを再生します。ディスプレイを持つクライアントは、メディアプレーヤー再生に関連する情報を表現する必要がある場合があります。その際、[`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo)イベントで再生メタデータをCICにリクエストし、`TemplateRuntime.RenderPlayerInfo`ディレクティブを受信します。`TemplateRuntime.RenderPlayerInfo`ディレクティブには、現在再生するメディアコンテンツと、後で再生するメディアコンテンツの再生メタデータが含まれます。クライアントは、`TemplateRuntime.RenderPlayerInfo`ディレクティブの再生メタデータをユーザーに提供して、現在再生しているメディアのメタデータおよび再生リストを表示することができます。ユーザーからリスト内の特定のメディアを再生するようにリクエストされたり、「いいね」([`TemplateRuntime.LikeCommandIssued`](#LikeCommandIssued))、「いいね」の取り消し([`TemplateRuntime.UnlikeCommandIssued`](#UnlikeCommandIssued))のような動作を処理する際、ベースとなるデータ(`token`)を提供します。

### Payload fields
| フィールド名       | データ型    | 説明                     | 常時/条件付き |
|---------------|---------|-----------------------------|:---------:|
| `displayType`               | string | メディアコンテンツを表示する形式。<ul><li><code>"list"</code>：リストで表示する</li><li><code>"single"</code>：1つのアイテムを表示する</li></ul>       | 常時 |
| `controls[]`                | object array | クライアントがメディアプレーヤーで表示すべきボタンの情報を持つオブジェクト配列です。             | 常時 |
| `controls[].enabled`        | boolean      | `controls[].name`で設定されたボタンを、メディアプレーヤーで有効にするかを示します。<ul><li><code>true</code>：有効にする</li><li><code>false</code>：無効にする</li></ul>  | 常時  |
| `controls[].name`           | string       | ボタンの名前。次のいずれかになります。<ul><li><code>"NEXT"</code>：「次」ボタン</li><li><code>"PLAY_PAUSE"</code>：「再生/一時停止」ボタン</li><li><code>"PREVIOUS"</code>：「前」ボタン</li></ul>  | 常時  |
| `controls[].selected`       | boolean      | メディアコンテンツが選択されているかを示します。この値は、ユーザーの「好き」という概念を表す際に使用することができます。この値が`true`に設定されていたら、ユーザーが好きなアイテムとして登録したコンテンツであることを示します。メディアプレーヤーの関連するUIで、そのことを表す必要があります。<ul><li><code>true</code>：選択済み</li><li><code>false</code>：未選択</li></ul> | 常時  |
| `controls[].type`           | string       | ボタンのタイプ。現在、`"BUTTON"`のみ使用します。  | 常時 |
| `playableItems[]`           | object array | 再生できるメディアコンテンツのリストを持つオブジェクト配列です。このフィールドは、空の配列の場合があります。  | 常時 |
| `playableItems[].artImageUrl`  | string    | メディアコンテンツ関連画像のURL。アルバムのジャケット画像や関連アイコンなどの画像があるURLです。      | 条件付き |
| `playableItems[].controls[]`                | object array  | 特定のメディアコンテンツを再生するとき、表示すべきボタンの情報を持つオブジェクト配列です。このオブジェクト配列は省略できます。  | 条件付き |
| `playableItems[].controls[].enabled`        | boolean      | `playableItems[].controls[].name`で設定されたボタンを、メディアプレーヤーで有効にするかを示します。<ul><li><code>true</code>：有効にする</li><li><code>false</code>：無効にする</li></ul>  | 常時  |
| `playableItems[].controls[].name`           | string       | ボタンの名前。次のいずれかになります。<ul><li><code>"NEXT"</code>：「次」ボタン</li><li><code>"PLAY_PAUSE"</code>：「再生/一時停止」ボタン</li><li><code>"PREVIOUS"</code>：「前」ボタン</li></ul>  | 常時  |
| `playableItems[].controls[].selected`       | boolean      | メディアコンテンツが選択されているかを示します。この値は、ユーザーの「好き」という概念を表す際に使用することができます。この値が`true`に設定されていたら、ユーザーが好きなアイテムとして登録したコンテンツであることを示します。メディアプレーヤーの関連するUIで、そのことを表す必要があります。<ul><li><code>true</code>：選択済み</li><li><code>false</code>：未選択</li></ul> | 常時  |
| `playableItems[].controls[].type`           | string       | ボタンのタイプ。現在、`"BUTTON"`のみ使用します。  | 常時 |
| `playableItems[].headerText`       | string        | 主に、現在の再生リストのタイトルを表すテキストフィールド                                                | 条件付き  |
| `playableItems[].lyrics[]`         | object array  | 歌詞のデータを持つオブジェクト配列。                                                            | 条件付き  |
| `playableItems[].lyrics[].data`    | string        | 歌詞のデータ。このフィールドと`playableItems[].lyrics[].url`フィールドのうち、1つは存在します。              | 条件付き  |
| `playableItems[].lyrics[].format`  | string        | 歌詞データの形式。<ul><li><code>"LRC"</code>：<a href="https://en.wikipedia.org/wiki/LRC_(file_format)" target="_blank">LRC形式</a></li><li><code>"PLAIN"</code>：テキスト形式</li></ul>  | 常時  |
| `playableItems[].lyrics[].url`     | string        | 歌詞データのURL。このフィールドと`playableItems[].lyrics[].data`フィールドのうち、1つは存在します。        | 条件付き  |
| `playableItems[].showAdultIcon`    | boolean       | 成人向けコンテンツを示すアイコンを表示するかどうか。<ul><li><code>true</code>：表示する。</li><li><code>false</code>：表示しない。</li></ul>   | 常時  |
| `playableItems[].titleSubText1`    | string        | 主にアーティスト名を表すテキストフィールド                                                          | 常時 |
| `playableItems[].titleSubText2`    | string        | 主にアルバム名を表すサブテキストフィールド                                                      | 条件付き |
| `playableItems[].titleText`        | string        | 現在のオーディオコンテンツのタイトルを表すテキストフィールド                                                         | 常時  |
| `playableItems[].token`            | string        | メディアコンテンツのトークン                                                                     | 常時 |
| `provider`                         | object        | メディアコンテンツ提供元の情報を持つオブジェクト                                                         | 条件付き |
| `provider.logoUrl`                 | string        | メディアコンテンツ提供元のロゴ画像のURL                                                         | 条件付き |
| `provider.name`                    | string        | メディアコンテンツ提供元の名前                                                                   | 常時  |
| `provider.smallLogoUrl`            | string        | メディアコンテンツ提供元のロゴ画像のURL                                                | 条件付き |

### Message example
{% raw %}

```json
// すぐに再生できるオーディオストリームのURL情報が含まれたサンプル
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

### 次の項目も参照してください。
* [`AudioPlayer.Play`](#Play)
* [`TemplateRuntime.LikeCommandIssued`](#LikeCommandIssued)
* [`TemplateRuntime.RequestPlayerInfo`](#RequestPlayerInfo)
* [`TemplateRuntime.UnlikeCommandIssued`](#UnlikeCommandIssued)

## RequestPlayerInfoIssuedイベント {#RequestPlayerInfoIssued}
クライアントから、メディアプレーヤーに表示する再生リスト、アルバムの画像、歌詞のような再生メタデータをCICにリクエストします。CICはこのイベントを受信すると、[`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo)ディレクティブをクライアントに送信します。


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`        | string  | 再生メタデータを読み取るとき、基準となるメディアコンテンツのトークン。[`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo)ディレクティブの`playableItems[].token`フィールドで提供されたトークンが入力される必要があります。 | 必須 |
| `range`        | object  | 再生メタデータの範囲を指定するオブジェクト。このフィールドが使用されていない場合、クライアントは任意の数のメタデータを受信します。   | 任意  |
| `range.before` | number  | 基準となるメディアコンテンツからn個前以前の再生リストに含まれた再生メタデータをリクエストします。  | 任意  |
| `range.after`  | number  | 基準となるメディアコンテンツからn個以降の再生リストに含まれた再生メタデータをリクエストします。例えば、`range.before`フィールドの値を指定しないで、`range.after`を`5`に設定すると、基準のメディアコンテンツを含めて、合計6つのメディアコンテンツに該当する再生メタデータを受信します。 | 任意  |

### 備考
* クライアントデバイスのボタンは、ハードウェア方式の物理ボタンの場合もあり、オーディオプレーヤーウィジェットのボタンのようなソフトウェア方式のボタンの場合もあります。

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

### 次の項目も参照してください。
* [`TemplateRuntime.ExpectRequestPlayerInfo`](#ExpectRequestPlayerInfo)
* [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo)

## UnlikeCommandIssuedイベント {#UnlikeCommandIssued}
ユーザーがクライアントのメディアプレーヤーで、特定のメディアに対して「いいね」を取り消すボタン(Unlike)を押した場合、クライアントはこのイベントをCICに送信する必要があります。CICはこのイベントを受信すると、適切なディレクティブをクライアントに送信します。


### Context fields

{% include "/CIC/References/CICInterface/Context_Objects_List.md" %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `token`    | string  | メディアコンテンツのトークン。[`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo)ディレクティブの`playableItems[].token`フィールドで提供されたトークンが入力される必要があります。 | 必須 |

### 備考
* クライアントデバイスのボタンは、ハードウェア方式の物理ボタンの場合もあり、オーディオプレーヤーウィジェットのボタンのようなソフトウェア方式のボタンの場合もあります。

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

### 次の項目も参照してください。
* [`TemplateRuntime.LikeCommandIssued`](#LikeCommandIssued)
* [`TemplateRuntime.RenderPlayerInfo`](#RenderPlayerInfo)
