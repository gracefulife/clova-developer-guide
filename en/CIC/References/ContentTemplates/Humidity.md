# Humidity template
Provides humidity information. It is used to display humidity readings on a screen.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> for an example of displaying humidity data.</p>
</div>

## Template field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| `bgClipUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object containing a URL of the background sound file | Yes |
| `humidity`  | [PercentageObject](/CIC/References/ContentTemplates/Shared_Objects.md#PercentageObject) | An object containing humidity data | No |
| `linkUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object containing a link path to the content  | No |
| `location`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing location information | Yes |
| `type`  | string | A content template delimiter. The value is always **"Humidity"**. | Yes |

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
<div class="midAlign"><img style="width: 300px !important" src="/CIC/Resources/Images/Content-Template-Humidity.png" /></div>

## See also
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)