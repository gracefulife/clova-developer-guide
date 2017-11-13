# WindSpeed template
Provides wind speeds. It is used to display wind speeds on a screen.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> on how wind speeds are displayed.</p>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `bgClipUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object containing URL of the background video file <div class="danger"><p><strong>Caution!</strong></p><p>Due to license issue, this field cannot be used from your partner company.</p></div> |
| `linkUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object containing a link path to the content. The `value` field of this object can have an empty string (`""`).   |
| `location`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing the location. The `value` field of this object can have an empty string (`""`).   |
| `type`          | string | A content template delimiter. The value is always "WindSpeed". |
| `windSpeed`     | [NumberObject](/CIC/References/ContentTemplates/Shared_Objects.md#NumberObject) | An object containing wind speeds. |

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

![WindSpeed](/CIC/Resources/Images/Content-Template-WindSpeed.png)

## See also
* [Atmosphere](/CIC/References/ContentTemplates/Atmosphere.md)
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/Humidity.md)
* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
