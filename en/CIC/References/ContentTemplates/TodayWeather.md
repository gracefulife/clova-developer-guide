# TodayWeather template

The TodayWeather template is used in providing today's weather information for the client to display on the client's screen.

<div class="note">
<p><strong>Note!</strong></p>
<p>See a <a href="#UIExample">UI example</a> on how the TodayWeather template is used in display.</p>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `bgClipUrl`                 | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | The URL of the video file to play in the background.<div class="danger"><p><strong>Caution!</strong></p><p>Due to a license issue, you are not permitted to use this URL.</p></div> |
| `concentrationOfFineDust`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The level of fine dust. |
| `houlyWeatherList[]` | object array | Contains hourly forecasts. |
| `houlyWeatherList[].hourlyTemperature` | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | The temperature. |
| `houlyWeatherList[].hourlyTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | The hour for which this weather forecast is provided for.  |
| `houlyWeatherList[].rainfallProbability` | [PercentageObject](/CIC/References/ContentTemplates/Shared_Objects.md#PercentageObject) | The chance of rain. A `null` indicates that this information is unavailable. |
| `houlyWeatherList[].temperatureImageCode` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)  | The [weather code](#WeatherCode) for this forecast. |
| `houlyWeatherList[].temperatureImageUrl` | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | The URL of the icon to represent this forecast. |
| `linkUrl`                   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | The link to open when the weather information is tapped. An empty string (`""`) indicates that this information is unavailable.  |
| `location`                  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The location this forecast is for. |
| `nowTemperature`            | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | The current temperature. |
| `nowWeather`                | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The current weather.  |
| `type`                      | string | The type of this template. The value is always `"TodayWeather"`. |

{% include "/CIC/References/ContentTemplates/Shared_Weather_Code.md" %}

## Template example

{% raw %}
```json
{
  "bgClipUrl": {
    "type": "url",
    "value": "https://ssl.pstatic.net/static/clova/service/weather/bg_clean_daytime.mp4"
  },
  "concentrationOfFineDust": {
    "type": "string",
    "value": "Moderate 29㎍/㎥"
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
    "value": "Shinjuku"
  },
  "nowTemperature": {
    "type": "temperature-c",
    "value": "31"
  },
  "nowWeather": {
    "type": "string",
    "value": "Sunny"
  },
  "type": "TodayWeather"
}
```
{% endraw %}

## UI example {#UIExample}

The following example shows how the TodayWeather template is used on the Clova app distributed by {{ book.OrientedService }}.

![TodayWeather](/CIC/Resources/Images/Content-Template-TodayWeather.png)

## See also

* [Atmosphere](/CIC/References/ContentTemplates/Atmosphere.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)
