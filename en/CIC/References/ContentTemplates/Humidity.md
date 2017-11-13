# Humidity template
Provides humidity information. It is used to display humidity on a screen.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> on how humidity is displayed.</p>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `bgClipUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object containing URL of the background video file. <div class="danger"><p><strong>Caution!</strong></p><p>Due to license issue, this field cannot be used from your partner company.</p></div> |
| `humidity`      | [PercentageObject](/CIC/References/ContentTemplates/Shared_Objects.md#PercentageObject) | An object containing humidity. |
| `linkUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object containing a link path to the content. The `value` field of this object can have an empty string (`""`).  |
| `location`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing the location. |
| `type`          | string | A content template delimiter. It has an `"Humidity"` value. |

## Template Example

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
    "value": "정자1동"
  },
  "type": "Humidity"
}
```
{% endraw %}

## Screen UI example {#UIExample}
The following example shows how the Humidity template is presented in the Clova mobile app distributed by {{ book.OrientedService }}.

![Humidity](/CIC/Resources/Images/Content-Template-Humidity.png)

## See also
* [Atmosphere](/CIC/References/ContentTemplates/Atmosphere.md)
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)
