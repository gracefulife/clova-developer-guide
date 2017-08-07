# WindSpeed Template
Provides information on wind speeds. It is used to display wind speeds on a screen.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> for an example of displaying wind speeds.</p>
</div>

## Template field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| bgClipUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object that contains a URL to a background sound file | Yes |
| linkUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object that contains a link path to content  | No |
| location  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains location data | Yes |
| type  | string | Content template delimiter. The value is always "WindSpeed" | Yes |
| windSpeed  | [NumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#NumberObject) | An object that contains wind speed data | No |

## Template Example

{% raw %}
```json
{
  "bgImageUrl": {
    "type": "url",
    "value": "https://ssl.pstatic.net/static/clova/service/weather/bg_cloud_night.mp4"
  },
  "location": {
    "type": "string",
    "value": "정자1동"
  },
  "type": "WindSpeed",
  "windSpeed": {
    "type": "number",
    "value": "1m/s"
  }
}
```
{% endraw %}

## Screen UI example {#UIExample}
The following example shows how the WindSpeed template is presented in the Clova mobile app distributed by {{ book.OrientedService }}.
<div class="midAlign"><img style="width: 300px !important" src="/CIC/Resources/Images/Content-Template-WindSpeed.png" /></div>

## See also
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/Humidity.md)
* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
