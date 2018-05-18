# Atmosphereテンプレート
大気情報を提供するテンプレートです。画面にPM10、PM2.5、オゾン、紫外線、黄砂の情報を表示するときに使用されます。

<div class="note">
<p><strong>メモ</strong></p>
<p>大気情報を表示するサンプルは、<a href="#UIExample">UI example</a>を参照してください。</p>
</div>

## Template fields

| フィールド名       | データ型    | 説明                     |
|---------------|---------|-----------------------------|
| `announcementOfAtmosphere`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 大気予報のテキストを持つオブジェクト。現在の大気の状況が表示される場合には省略されます。省略される場合、このオブジェクトの`value`フィールドは空文字列(`""`)を持ちます。 |
| `bgClipUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 背景動画ファイルのURLを持つオブジェクト。<div class="danger"><p><strong>注意</strong></p><p>このフィールドのデータは、ライセンスの問題により、提携会社では使用できません。</p></div> |
| `concentrationOfAtmosphere` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 現在の大気の状況、または空気質の指数を持つオブジェクト。予報の場合には省略されます。省略される場合、このオブジェクトの`value`フィールドは空文字列(`""`)を持ちます。 |
| `contentProviderText`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | コンテンツ提供元の情報を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。  |
| `halfDayAtmosphereList[]`             | object array | 半日(午前/午後)ごとの大気情報を持つオブジェクト配列                                    |
| `halfDayAtmosphereList[].atmosphereImageUrl` | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | `halfDayAtmosphereList[].durationHalfDay`フィールドに入力された時間帯の大気の状況を表示する画像ファイルのURLを持つオブジェクト |
| `halfDayAtmosphereList[].concentrationOfAtmosphere`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | `halfDayAtmosphereList[].durationHalfDay`に入力された時間帯の大気の状況または空気質の指数を持つオブジェクト  |
| `halfDayAtmosphereList[].durationHalfDay`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 大気情報を表示する時間の範囲を持つオブジェクト。このオブジェクトの`value`フィールドは、`明日の午前`、`明日の午後`、`明後日の午前`、`明後日の午後`のような値を持ちます。  |
| `lastUpdate`                | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | 天気情報の最終更新時間を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `linkUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | コンテンツのリンク先のURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。  |
| `location`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 地域の情報を持つオブジェクト |
| `referenceText`             | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 参照したサービスの情報を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。  |
| `referenceUrl`              | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 参照したサービスの利用結果ページのURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。   |
| `temperatureCode`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | [天気コード](#WeatherCode)を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。  |
| `type`          | string | コンテンツテンプレートのタイプを示す値。`"Atmosphere"`を持ちます。 |
| `valueOfAtmosphere`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 現在の大気の数値を持つオブジェクト。数値の単位が含まれています。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |

## Template example

{% raw %}
```json
// 現在の大気情報
{
  "announcementOfAtmosphere": {
    "type": "string",
    "value": ""
  },
  "bgClipUrl": {
    "type": "url",
    "value": "https://ssl.pstatic.net/static/clova/service/weather/bg_clean_daytime.mp4"
  },
  "concentrationOfAtmosphere": {
    "type": "string",
    "value": "良好"
  },
  "contentProviderText" : {
    "type" : "string",
    "value" : "気象庁"
  },
  "failureMessage": {
    "type": "string",
    "value": "京畿道城南市盆唐区亭子1洞の現在のPM10指数は、良好です"
  },
  "halfDayAtmosphereList": [
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.contentproviderdomain.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "普通"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "明日の午前"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.contentproviderdomain.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "普通"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "明日の午後"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.contentproviderdomain.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "普通"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "明後日の午前"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.contentproviderdomain.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "普通"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "明後日の午後"
      }
    }
  ],
  "location": {
    "type": "string",
    "value": "亭子1洞"
  },
  "meta": {
    "version": {
      "type": "string",
      "value": "v0.1"
    }
  },
  "lastUpdate" : {
    "type" : "datetime",
    "value" : "2018-02-05T06:29:09Z"
  },
  "referenceText" : {
    "type" : "string",
    "value" : "NAVER天気"
  },
  "referenceUrl" : {
    "type" : "url",
    "value" : "http://weather.contentproviderdomain.com/"
  },
  "temperatureCode": {
    "type": "string",
    "value": "5"
  },
  "type": "Atmosphere",
  "valueOfAtmosphere": {
    "type": "number",
    "value": "27㎍/㎥"
  }
}

// 明日の大気の状況
{
  "announcementOfAtmosphere": {
    "type": "string",
    "value": "明日は、PM10の指数が高いでしょう"
  },
  "bgClipUrl": {
    "type": "url",
    "value": "https://ssl.pstatic.net/static/clova/service/weather/bg_cloud_daytime.mp4"
  },
  "concentrationOfAtmosphere": {
    "type": "string",
    "value": ""
  },
  "failureMessage": {
    "type": "string",
    "value": "京畿道城南市盆唐区亭子1洞の現在のPM10指数は、普通です"
  },
  "halfDayAtmosphereList": [
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.contentproviderdomain.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "普通"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "明日の午前"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.contentproviderdomain.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "普通"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "明日の午後"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.contentproviderdomain.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "普通"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "明後日の午前"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.contentproviderdomain.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "普通"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "明後日の午後"
      }
    }
  ],
  "location": {
    "type": "string",
    "value": "亭子1洞"
  },
  "meta": {
    "version": {
      "type": "string",
      "value": "v0.1"
    }
  },
  "type": "Atmosphere",
  "valueOfAtmosphere": {
    "type": "number",
    "value": ""
  }
}
```
{% endraw %}

## UI example {#UIExample}
以下は、{{ book.OrientedService }}が配布したClovaのモバイルアプリで、Atmosphereテンプレートの内容を表したUIサンプルです。

| 現在の大気の状況 | 明日の大気の状況 |
|-------------|------------|
| ![Now](/CIC/Resources/Images/Content-Template-Atmosphere_Now.png) | ![Original](/CIC/Resources/Images/Content-Template-Atmosphere_Tomorrow.png) |

## 次の項目も参照してください。
* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)
