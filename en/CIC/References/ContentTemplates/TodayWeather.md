# TodayWeather template
Provides weather forecasts for today. It is used to display today's weather on a screen.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> on how today's weather is displayed.</p>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `bgClipUrl`                 | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object containing URL of the background video file. <div class="danger"><p><strong>Caution!</strong></p><p>Due to license issue, this field cannot be used by your partner company.</p></div> |
| `concentrationOfFineDust`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing fine dust concentrations level data. |
| `houlyWeatherList[]` | object array | An object array containing hourly weather. |
| `houlyWeatherList[].hourlyTemperature` | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | An object containing hourly temperature. |
| `houlyWeatherList[].hourlyTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | An object containing hourly time. |
| `houlyWeatherList[].rainfallProbability` | [PercentageObject](/CIC/References/ContentTemplates/Shared_Objects.md#PercentageObject) | An object containing rainfall probability. The `value` field of this object can have a `null` value. |
| `houlyWeatherList[].temperatureImageCode` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing [weather codes](#WeatherCode) for hourly weather. |
| `houlyWeatherList[].temperatureImageUrl` | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object containing URL of a file displaying images of hourly weather. |
| `linkUrl`                   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object containing a link path to the content. The `value` field of this object can have an empty string (`""`).   |
| `location`                  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing the location. |
| `nowTemperature`            | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | An object containing current temperature. |
| `nowWeather`                | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing current weather.  |
| `type`                      | string | A content template delimiter. It has an `"TodayWeather"` value. |

{% include "./Shared_Weather_Code.md" %}

## Template Example

{% raw %}
```json
{
  "bgClipUrl": {
    "type": "url",
    "value": "https://ssl.pstatic.net/static/clova/service/weather/bg_clean_daytime.mp4"
  },
  "concentrationOfFineDust": {
    "type": "string",
    "value": "좋음 29㎍/㎥"
  },
  "hourlyWeatherList": [
    {
      "hourlyTemperature": {
        "type": "temperature",
        "value": "30"
      },
      "hourlyTime": {
        "type": "datetime",
        "value": "20170726 18:00"
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
        "type": "temperature",
        "value": "27"
      },
      "hourlyTime": {
        "type": "datetime",
        "value": "20170726 21:00"
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
        "type": "temperature",
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
        "type": "temperature",
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
        "type": "temperature",
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
        "type": "temperature",
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
        "type": "temperature",
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
        "type": "temperature",
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
        "type": "temperature",
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
        "type": "temperature",
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
    }
  ],
  "location": {
    "type": "string",
    "value": "정자1동"
  },
  "nowTemperature": {
    "type": "temperature-c",
    "value": "31"
  },
  "nowWeather": {
    "type": "string",
    "value": "맑음"
  },
  "type": "TodayWeather"
}
```
{% endraw %}

## Screen UI example {#UIExample}
The following example shows how the TodayWeather template is presented in the Clova mobile app distributed by {{ book.OrientedService }}.

![TodayWeather](/CIC/Resources/Images/Content-Template-TodayWeather.png)

## See also
* [Atmosphere](/CIC/References/ContentTemplates/Atmosphere.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)
