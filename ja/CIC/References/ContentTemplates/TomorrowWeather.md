# TomorrowWeatherテンプレート
明日の天気情報を提供するテンプレートです。画面に明日の天気情報を表示するときに使用されます。

<div class="note">
<p><strong>メモ</strong></p>
<p>明日の天気を表示するサンプルは、<a href="#UIExample">UI example</a>を参照してください。</p>
</div>

## Template fields

| フィールド名       | データ型    | 説明                     |
|---------------|---------|-----------------------------|
| `bgClipUrl`                 | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 背景動画ファイルのURLを持つオブジェクト。<div class="danger"><p><strong>注意</strong></p><p>このフィールドのデータは、ライセンスの問題により、提携会社では使用できません。</p></div> |
| `contentProviderText`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | コンテンツ提供元の情報を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。  |
| `highTemperature`           | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | 明日の最高気温を持つオブジェクト |
| `highTempWeather`           | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 気温が一番高いときの天気情報を持つオブジェクト  |
| `houlyWeatherList[]` | object array | 時間ごとの天気情報を持つオブジェクト配列 |
| `houlyWeatherList[].hourlyTemperature` | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | 時間ごとの気温情報を持つオブジェクト |
| `houlyWeatherList[].hourlyTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | 時間ごとの情報を持つオブジェクト |
| `houlyWeatherList[].rainfallProbability` | [PercentageObject](/CIC/References/ContentTemplates/Shared_Objects.md#PercentageObject) | 降水確率を持つオブジェクト。このオブジェクトの`value`フィールドは、`null`値を持つ場合があります。      |
| `houlyWeatherList[].temperatureImageCode` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 時間ごとの[天気コード](#WeatherCode)を持つオブジェクト |
| `houlyWeatherList[].temperatureImageUrl` | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 時間ごとの天気の画像ファイルのURLを持つオブジェクト |
| `lastUpdate`                | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | 天気情報の最終更新時間を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `linkUrl`                   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | コンテンツのリンク先のURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。      |
| `location`                  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 地域の情報を持つオブジェクト |
| `lowTemperature`           | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | 明日の最低気温を持つオブジェクト |
| `lowTempWeather`           | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 気温が一番低いときの天気情報を持つオブジェクト  |
| `referenceText`             | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 参照したサービスの情報を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。  |
| `referenceUrl`              | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 参照したサービスの利用結果ページのURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。   |
| `type`                      | string | コンテンツテンプレートのタイプを示す値。`"TomorrowWeather"`を持ちます。 |

{% include "/CIC/References/ContentTemplates/Shared_Weather_Code.md" %}

## Template example

{% raw %}
```json
{
  "bgClipUrl": {
    "type": "url",
    "value": "https://ssl.pstatic.net/static/clova/service/weather/bg_cloud_daytime.mp4"
  },
  "highTempWeather": {
    "type": "string",
    "value": "曇り"
  },
  "highTemperature": {
    "type": "temperature-c",
    "value": "32"
  },
  "hourlyWeatherList": [
    {
      "hourlyTemperature": {
        "type": "temperature-c",
        "value": "25"
      },
      "hourlyTime": {
        "type": "datetime",
        "value": "20170727 00:00"
      },
      "rainfallProbability": {
        "type": "percentage",
        "value": "20%"
      },
      "temperatureImageCode": {
        "type": "string",
        "value": "5"
      },
      "temperatureImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      }
    },
    {
      "hourlyTemperature": {
        "type": "temperature-c",
        "value": "23"
      },
      "hourlyTime": {
        "type": "datetime",
        "value": "20170727 03:00"
      },
      "rainfallProbability": {
        "type": "percentage",
        "value": "20%"
      },
      "temperatureImageCode": {
        "type": "string",
        "value": "5"
      },
      "temperatureImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      }
    },
    {
      "hourlyTemperature": {
        "type": "temperature-c",
        "value": "23"
      },
      "hourlyTime": {
        "type": "datetime",
        "value": "20170727 06:00"
      },
      "rainfallProbability": {
        "type": "percentage",
        "value": "20%"
      },
      "temperatureImageCode": {
        "type": "string",
        "value": "5"
      },
      "temperatureImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      }
    },
    {
      "hourlyTemperature": {
        "type": "temperature-c",
        "value": "25"
      },
      "hourlyTime": {
        "type": "datetime",
        "value": "20170727 09:00"
      },
      "rainfallProbability": {
        "type": "percentage",
        "value": "20%"
      },
      "temperatureImageCode": {
        "type": "string",
        "value": "5"
      },
      "temperatureImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      }
    },
    {
      "hourlyTemperature": {
        "type": "temperature-c",
        "value": "27"
      },
      "hourlyTime": {
        "type": "datetime",
        "value": "20170727 12:00"
      },
      "rainfallProbability": {
        "type": "percentage",
        "value": "20%"
      },
      "temperatureImageCode": {
        "type": "string",
        "value": "5"
      },
      "temperatureImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      }
    },
    {
      "hourlyTemperature": {
        "type": "temperature-c",
        "value": "29"
      },
      "hourlyTime": {
        "type": "datetime",
        "value": "20170727 15:00"
      },
      "rainfallProbability": {
        "type": "percentage",
        "value": "20%"
      },
      "temperatureImageCode": {
        "type": "string",
        "value": "5"
      },
      "temperatureImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      }
    },
    {
      "hourlyTemperature": {
        "type": "temperature-c",
        "value": "28"
      },
      "hourlyTime": {
        "type": "datetime",
        "value": "20170727 18:00"
      },
      "rainfallProbability": {
        "type": "percentage",
        "value": "20%"
      },
      "temperatureImageCode": {
        "type": "string",
        "value": "5"
      },
      "temperatureImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      }
    },
    {
      "hourlyTemperature": {
        "type": "temperature-c",
        "value": "26"
      },
      "hourlyTime": {
        "type": "datetime",
        "value": "20170727 21:00"
      },
      "rainfallProbability": {
        "type": "percentage",
        "value": "20%"
      },
      "temperatureImageCode": {
        "type": "string",
        "value": "5"
      },
      "temperatureImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      }
    },
    {
      "hourlyTemperature": {
        "type": "temperature-c",
        "value": "26"
      },
      "hourlyTime": {
        "type": "datetime",
        "value": "20170728 00:00"
      },
      "rainfallProbability": {
        "type": "percentage",
        "value": "20%"
      },
      "temperatureImageCode": {
        "type": "string",
        "value": "5"
      },
      "temperatureImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      }
    },
    {
      "hourlyTemperature": {
        "type": "temperature-c",
        "value": "24"
      },
      "hourlyTime": {
        "type": "datetime",
        "value": "20170728 03:00"
      },
      "rainfallProbability": {
        "type": "percentage",
        "value": "80%"
      },
      "temperatureImageCode": {
        "type": "string",
        "value": "9"
      },
      "temperatureImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_09.png"
      }
    }
  ],
  "location": {
    "type": "string",
    "value": "亭子1洞"
  },
  "lowTempWeather": {
    "type": "string",
    "value": "曇り"
  },
  "lowTemperature": {
    "type": "temperature-c",
    "value": "23"
  },
  "contentProviderText" : {
    "type" : "string",
    "value" : "気象庁"
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
  "type": "TomorrowWeather"
}
```
{% endraw %}

## UI example {#UIExample}
以下は、{{ book.OrientedService }}が配布したClovaのモバイルアプリで、TomorrowWeatherテンプレートの内容を表したUIサンプルです。

![TomorrowWeather](/CIC/Resources/Images/Content-Template-TomorrowWeather.png)

## 次の項目も参照してください。
* [Atmosphere](/CIC/References/ContentTemplates/Atmosphere.md)
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)
