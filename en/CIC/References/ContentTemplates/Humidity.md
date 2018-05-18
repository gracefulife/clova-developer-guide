# Humidity Template
The Humidity template is used in providing humidity information for the client to display on the client screen.

<div class="note">
<p><strong>Note!</strong></p>
<p>See a <a href="#UIExample">UI example</a> of the Humidity template used in display.</p>
</div>

## Template fields

| Field name       | Data type    | Description                     |
|---------------|---------|-----------------------------|
| `bgClipUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | The URL of the video file to play in the background. <div class="danger"><p><strong>Caution!</strong></p><p>Due to a license issue, you are not permitted to use this URL.</p></div> |
| `contentProviderText`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The information of the content provider. An empty string (`""`) indicates that no content is to be displayed.  |
| `humidity`      | [PercentageObject](/CIC/References/ContentTemplates/Shared_Objects.md#PercentageObject) | The information on humidity. |
| `lastUpdate`                | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | The last update time of the weather information. An empty string (`""`) indicates that no content is to be displayed. |
| `linkUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | The URL of the content. An empty string (`""`) indicates that no content is to be displayed.  |
| `location`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The information on the region. |
| `referenceText`             | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The information of the referred service. An empty string (`""`) indicates that no content is to be displayed.  |
| `referenceUrl`              | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The information on the usage result URL of the referred service. An empty string (`""`) indicates that no content is to be displayed.   |
| `temperatureCode`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The information on the [weather code](#WeatherCode). An empty string (`""`) indicates that no content is to be displayed.  |
| `type`          | string | The type of this template. The value is always `"Humidity"`. |

## Template example

{% raw %}
```json
{
  "bgImageUrl": {
    "type": "url",
    "value": "https://ssl.pstatic.net/static/clova/service/weather/bg_cloud_night.mp4"
  },
  "humidity": {
    "type": "percentage",
    "value": "60%"
  },
  "location": {
    "type": "string",
    "value": "Jeongja1-dong"
  },
  "contentProviderText" : {
    "type" : "string",
    "value": "National weather service"
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
    "value": "NAVER weather"
  },
  "referenceUrl" : {
    "type" : "url",
    "value" : "http://weather.contentproviderdomain.com/"
  },
  "type": "Humidity"
}
```
{% endraw %}

## UI example {#UIExample}
The following example shows how the Humidity template is used on the Clova app distributed by {{ book.OrientedService }}.

![Humidity](/CIC/Resources/Images/Content-Template-Humidity.png)

## See also
* [Atmosphere](/CIC/References/ContentTemplates/Atmosphere.md)
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)
