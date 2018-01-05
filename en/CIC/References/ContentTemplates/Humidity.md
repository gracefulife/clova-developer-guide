# Humidity template

The Humidity template is used in providing humidity information for the client to display on the client's screen.

<div class="note">
<p><strong>Note!</strong></p>
<p>See a <a href="#UIExample">UI example</a> of the Humidity template used in display.</p>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `bgClipUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | The URL of the video file to play in the background. <div class="danger"><p><strong>Caution!</strong></p><p>Due to a license issue, you are not permitted to use this URL.</p></div> |
| `humidity`      | [PercentageObject](/CIC/References/ContentTemplates/Shared_Objects.md#PercentageObject) | The humidity. |
| `linkUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | The URL of the content to display when the humidity information is tapped. An empty string (`""`) indicates that no content is to be displayed. |
| `location`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The location which the humidity information is for.  |
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
    "value": "Shinjuku"
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
