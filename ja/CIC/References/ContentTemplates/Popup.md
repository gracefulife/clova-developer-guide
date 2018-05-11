# Popupテンプレート
Toast、alert、popupで表示するテキストやボタンの情報を提供するテンプレートです。表示形式によって、有効なフィールドが異なる場合があります。

| 表示形式       | 説明                      | 有効なフィールド                         |
|---------------|-----------------------------|-----------------------------|
| Toast         | テキストと、関連するリンクで構成されるtoastです。    | `toastLinkText`、`toastLinkUrl`、`toastText`                  |
| Alert         | テキストと確認ボタンで構成されるalertです。   | `alertText`                                                   |
| Popup(1つのボタン) | タイトル、テキスト、ボタン(リンク)で構成されるpopupです。 | `mainText`、`positiveButtonText`、`positiveButtonUrl`、`title`   |
| Popup(2つのボタン) | タイトル、テキスト、2つのボタンで構成されるpopupです。 | `negativeButtonText`、`negativeButtonUrl`、`mainText`、`positiveButtonText`、`positiveButtonUrl`、`title` |

<div class="note">
<p><strong>メモ</strong></p>
<p>Popupテンプレートの表示形式については、<a href="#UIExample">UI example</a>を参照してください。</p>
</div>

## Template fields

| フィールド名       | データ型    | 説明                     |
|---------------|---------|-----------------------------|
| `alertText`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Alertに表示する注意テキストを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `displayType`      | string                                                                          | 表示する画面の種類。以下の値を持つことができます。<ul><li><code>"POPUP"</code></li><li><code>"ALERT"</code></li><li><code>"TOAST"</code></li></ul>  |
| `negativeButtonText`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Popupで、**いいえ**などの否定ボタンに表示するテキストを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `negativeButtonUrl`    | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | Popupで、**いいえ**などの否定ボタンにリンクするURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `mainText`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Popupに表示するテキストを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `positiveButtonText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Popupで、**はい**などの肯定ボタンに表示するテキストを持つオブジェクト。1つのボタンを持つpopupの場合、**OK**のような意味を持つボタンに表示するテキストとして、このオブジェクトを使用します。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `positiveButtonUrl`   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | Popupで、**はい**など、肯定ボタンにリンクするURLを持つオブジェクト。1つのボタンを持つpopupの場合、**OK**のような意味を持つボタンにリンクするURLとして、このオブジェクトを使用します。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `title`            | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Popupに表示するタイトルを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `toastLinkText`    | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Toastに表示するリンクのテキストを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `toastLinkUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | Toastに表示するリンクのURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `toastText`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Toastに表示するテキストを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `type`             | string                                                                          | コンテンツテンプレートのタイプを示す値。`"Popup"`を持ちます。     |

## Template example

{% raw %}
```json
// サンプル1. Toast形式
{
  "type": "Popup",
  "displayType": "TOAST",
  "toastText": {
    "type": "string",
    "value": "1分のプレビュー再生中です。あなたの音楽の好みに合わせるイベントに参加して、NAVERミュージック100曲利用クーポンをGETしよう!"
  },
  "toastLinkText": {
    "type": "string",
    "value": "イベントに参加する >"
  },
  "toastLinkUrl": {
    "type": "url",
    "value": "https://..."
  },
  "alertText": {
    "type": "string",
    "value": ""
  },
  "title": {
    "type": "string",
    "value": ""
  },
  "mainText": {
    "type": "string",
    "value": ""
  },
  "negativeButtonText": {
    "type": "string",
    "value": ""
  },
  "negativeButtonUrl": {
    "type": "url",
    "value": ""
  },
  "positiveButtonText": {
    "type": "string",
    "value": ""
  },
  "positiveButtonUrl": {
    "type": "url",
    "value": ""
  }
}

// サンプル2. Alert形式
{
  "type": "Popup",
  "displayType": "ALERT",
  "toastText": {
    "type": "string",
    "value": ""
  },
  "toastLinkText": {
    "type": "string",
    "value": ""
  },
  "toastLinkUrl": {
    "type": "url",
    "value": ""
  },
  "alertText": {
    "type": "string",
    "value": "別のデバイスで再生を開始したため、音楽の再生が中止されました。"
  },
  "title": {
    "type": "string",
    "value": ""
  },
  "mainText": {
    "type": "string",
    "value": ""
  },
  "negativeButtonText": {
    "type": "string",
    "value": ""
  },
  "negativeButtonUrl": {
    "type": "url",
    "value": ""
  },
  "positiveButtonText": {
    "type": "string",
    "value": ""
  },
  "positiveButtonUrl": {
    "type": "url",
    "value": ""
  }
}

// サンプル3. 1つのボタンを持つpopup形式
{
  "type": "Popup",
  "displayType": "POPUP",
  "toastText": {
    "type": "string",
    "value": ""
  },
  "toastLinkText": {
    "type": "string",
    "value": ""
  },
  "toastLinkUrl": {
    "type": "url",
    "value": ""
  },
  "alertText": {
    "type": "string",
    "value": ""
  },
  "title": {
    "type": "string",
    "value": "あなたの好みはもうコンプリート!"
  },
  "mainText": {
    "type": "string",
    "value": "NAVERミュージック100曲利用クーポンで、クローバーがおすすめする音楽を楽しんでくださいね!"
  },
  "negativeButtonText": {
    "type": "string",
    "value": ""
  },
  "negativeButtonUrl": {
    "type": "url",
    "value": ""
  },
  "positiveButtonText": {
    "type": "string",
    "value": "ミュージック100曲利用クーポンを獲得する"
  },
  "positiveButtonUrl": {
    "type": "url",
    "value": "https://..."
  }
}

// サンプル4. 2つのボタンを持つpopup形式
{
  "type": "Popup",
  "displayType": "POPUP",
  "toastText": {
    "type": "string",
    "value": ""
  },
  "toastLinkText": {
    "type": "string",
    "value": ""
  },
  "toastLinkUrl": {
    "type": "url",
    "value": ""
  },
  "alertText": {
    "type": "string",
    "value": ""
  },
  "title": {
    "type": "string",
    "value": "あなたの好みはもうコンプリート!"
  },
  "mainText": {
    "type": "string",
    "value": "あなたの音楽の好みがわかったので、これから良い曲をどんどんおすすめしますよ。"
  },
  "negativeButtonText": {
    "type": "string",
    "value": "続ける"
  },
  "negativeButtonUrl": {
    "type": "url",
    "value": "https://..."
  },
  "positiveButtonText": {
    "type": "string",
    "value": "終了する"
  },
  "positiveButtonUrl": {
    "type": "url",
    "value": "https://..."
  }
}
```
{% endraw %}

## UI example {#UIExample}
以下は、{{ book.OrientedService }}が配布したClovaのモバイルアプリで、Popupテンプレートの内容を表したUIサンプルです。

| Toast形式 | Alert形式 |
|-----------|-----------|
| ![Type1](/CIC/Resources/Images/Content-Template-Toast.png) | ![Type2](/CIC/Resources/Images/Content-Template-Alert.png) |

| Popup(1つのボタン) | Popup(2つのボタン) |
|-------------------|--------------------|
| ![Type3](/CIC/Resources/Images/Content-Template-Popup_with_One_Button.png) | ![Type](/CIC/Resources/Images/Content-Template-Popup_with_Two_Buttons.png) |

## 次の項目も参照してください。
* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
* [Text](/CIC/References/ContentTemplates/Text.md)
