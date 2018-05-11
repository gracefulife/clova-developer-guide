# ImageTextテンプレート
画面に表示する画像とテキストデータを一緒に提供するテンプレートです。サムネイル画像とテキストを表示したり、地図とテキストを一緒に表示したりするときに使用されます。

<div class="note">
<p><strong>メモ</strong></p>
<p>ImageTextテンプレートの表示形式については、<a href="#UIExample">UI example</a>を参照してください。</p>
</div>

## Template fields

| フィールド名       | データ型    | 説明                     |
|---------------|---------|-----------------------------|
| `appLinkUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | 地図の画像が含まれた場合、{{ book.OrientedService }}マップアプリに移動するURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。  |
| `imageUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | 画像のURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。                                |
| `linkUrl`        | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | 地図の画像が含まれた場合、ウェブの地図に移動するURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。   |
| `mainText`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | メインテキストを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。                                       |
| `referenceText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | 参照したサービスの情報を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。  |
| `referenceUrl`   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | 参照したサービスの利用結果ページのURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。   |
| `subTextList[]`    | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | サブテキストを持つオブジェクト配列。このオブジェクト配列の要素の`value`フィールドは、空文字列(`""`)を持つ場合があります。                               |
| `thumbImageUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | サムネイル画像のURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。                           |
| `thumbImageType` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | サムネイル画像のタイプを持つオブジェクトで、以下の値を持ちます。<ul><li><code>"人物"</code>：人物</li><li><code>"書籍"</code>：書籍</li><li><code>"アルバムジャケット"</code>：アルバムジャケット</li><li>空文字列(<code>""</code>)：サムネイル情報なし</li></ul> |
| `type`           | string  | コンテンツテンプレートのタイプを示す値。`"ImageText"`を持ちます。      |

## Template example

{% raw %}

```json
// サンプル1.
// ユーザーのリクエスト：リオネル・メッシの所属チームは? (サムネイル画像とテキストを表示する)
{
  "type": "ImageText",
  "imageUrl": {
    "type": "url",
    "value": ""
  },
  "mainText": {
    "type": "string",
    "value": "リオネル・メッシ"
  },
  "referenceText": {
    "type": "string",
    "value": "NAVER検索結果"
  },
  "referenceUrl": {
    "type": "url",
    "value": "https://m.search.contentproviderdomain.com/search?where=m&sm=mob_lic&query=%eb%a6%ac%ec%98%a4%eb%84%ac+%eb%a9%94%ec%8b%9c+%ec%86%8c%ec%86%8d%ed%8c%80"
  },
  "subTextList": [
    {
      "type": "string",
      "value": "FCバルセロナ"
    }
  ],
  "thumbImageType": {
    "type": "string",
    "value": "人物"
  },
  "thumbImageUrl": {
    "type": "url",
    "value": "http://sstatic.contentproviderdomain.net/people/3/201607071816066361.jpg"
  }
}

// サンプル2.
// ユーザーのリクエスト：現在位置を教えて(地図の画像とテキストを表示する)
{
  "appLinkUrl": {
    "type": "url",
    "value": "nmap://map?lat=37.3594589&lng=127.1047745&level=13&mode=1&traffic=false&bicycle=false&cadastral=false&appname=com.contentproviderdomain.clova"
  },
  "imageUrl": {
    "type": "url",
    "value": "https://simg.pstatic.net/static.map/image?caller=mw_search&crs=EPSG:4326&scale=2&format=jpg&dataversion=163.2&version=1.1&baselayer=default&center=127.1047745,37.3594589&markers=type,default2_s,127.1047745,37.3594589&level=10&h=402&w=515"
  },
  "linkUrl": {
    "type": "url",
    "value": "https://m.map.contentproviderdomain.com/map.nhn?lat=37.3594589&lng=127.1047745&dlevel=&mapMode=&pinTitle=&boundary=&traffic="
  },
  "mainText": {
    "type": "string",
    "value": "京畿道城南市盆唐区亭子1洞"
  },
  "meta": {
    "version": {
      "type": "string",
      "value": "v0.1"
    }
  },
  "referenceText": {
    "type": "string",
    "value": "NAVER検索結果"
  },
  "referenceUrl": {
    "type": "url",
    "value": "https://m.search.contentproviderdomain.com/search?where=m&sm=mob_lic&query=%ed%98%84%ec%9e%ac+%ec%9c%84%ec%b9%98"
  },
  "subTextList": [
    {
      "type": "string",
      "value": ""
    }
  ],
  "thumbImageType": {
    "type": "string",
    "value": ""
  },
  "thumbImageUrl": {
    "type": "url",
    "value": ""
  },
  "type": "ImageText"
}
```

{% endraw %}

## UI example {#UIExample}
以下は、{{ book.OrientedService }}が配布したClovaのモバイルアプリで、ImageTextテンプレートの内容を表したUIサンプルです。

| サムネイル画像とテキスト | 地図の画像とテキスト |
|-------|-------|
| ![Thumbnail](/CIC/Resources/Images/Content_Template-Thumbimage_and_Text.png) | ![Map and text](/CIC/Resources/Images/Content_Template-Mapimage_and_Text.png) |

## 次の項目も参照してください。
* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [Popup](/CIC/References/ContentTemplates/Popup.md)
* [Text](/CIC/References/ContentTemplates/Text.md)
