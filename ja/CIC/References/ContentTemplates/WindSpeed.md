# WindSpeedテンプレート
風速情報を提供するテンプレートです。画面に風速を表示するときに使用されます。

<div class="note">
<p><strong>メモ</strong></p>
<p>風速を表示するサンプルは、<a href="#UIExample">UI example</a>を参照してください。</p>
</div>

## Template fields

| フィールド名       | データ型    | 説明                     |
|---------------|---------|-----------------------------|
| `bgClipUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 背景動画ファイルのURLを持つオブジェクト。<div class="danger"><p><strong>注意</strong></p><p>このフィールドのデータは、ライセンスの問題により、提携会社では使用できません。</p></div> |
| `contentProviderText`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | コンテンツ提供元の情報を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。  |
| `lastUpdate`                | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | 天気情報の最終更新時間を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。 |
| `linkUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | コンテンツのリンク先のURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。   |
| `location`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 地域の情報を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。   |
| `referenceText`             | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 参照したサービスの情報を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。  |
| `referenceUrl`              | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 参照したサービスの利用結果ページのURLを持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。   |
| `temperatureCode`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | [天気コード](#WeatherCode)を持つオブジェクト。このオブジェクトの`value`フィールドは、空文字列(`""`)を持つ場合があります。  |
| `type`          | string | コンテンツテンプレートのタイプを示す値。"WindSpeed"に固定されています。 |
| `windDirection` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 風向き情報を持つオブジェクト。 |
| `windSpeed`     | [NumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#NumberObject) | 風速情報を持つオブジェクト。 |

## Template example

{% raw %}
```json
{
  "bgImageUrl": {
    "type": "url",
    "value": "https://ssl.pstatic.net/static/clova/service/weather/bg_cloud_night.mp4"
  },
  "location": {
    "type": "string",
    "value": "亭子1洞"
  },
  "contentProviderText" : {
    "type" : "string",
    "value" : "気象庁"
  },
  "temperatureCode": {
    "type": "string",
    "value": "5"
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
  "type": "WindSpeed",
  "windDirection": {
    "type": "string",
    "value": "W"
  },
  "windSpeed": {
    "type": "number",
    "value": "1m/s"
  }
}
```
{% endraw %}

## UI example {#UIExample}
以下は、{{ book.OrientedService }}が配布したClovaのモバイルアプリで、WindSpeedテンプレートの内容を表したUIサンプルです。

![WindSpeed](/CIC/Resources/Images/Content-Template-WindSpeed.png)

## 次の項目も参照してください。
* [Atmosphere](/CIC/References/ContentTemplates/Atmosphere.md)
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/Humidity.md)
* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
