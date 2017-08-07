# TomorrowWeather Template
Provides weather information for tomorrow. It is used to display tomorrow's weather on a screen.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> for an example of displaying tomorrow's weather.</p>
</div>

## Template field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| bgClipUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object that contains a URL to a background sound file | Yes |
| highTemperature  | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | An object that contains the highest temperature tomorrow afternoon | Yes |
| highTempWeather  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains weather data when the temperature is at the highest  | Yes |
| houlyWeatherList[] | object array | An object array that contains hourly weather data | Yes |
| houlyWeatherList[].hourlyTemperature | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | An object that contains hourly temperature data | Yes |
| houlyWeatherList[].hourlyTime | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | An object that contains time data | Yes |
| houlyWeatherList[].rainfallProbability | [PercentageObject](/CIC/References/ContentTemplates/Shared_Objects.md#PercentageObject) | An object that contains rainfall probability | No |
| houlyWeatherList[].temperatureImageCode | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains hourly [weather code](#WeatherCode) | Yes |
| houlyWeatherList[].temperatureImageUrl | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object that contains a URL to image files for hourly weather | Yes |
| linkUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object that contains a link path to content  | No |
| location  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains location data | Yes |
| lowTemperature  | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | An object that contains the lowest temperature tomorrow morning | Yes |
| lowTempWeather  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains weather data when the temperature is at the lowest  | Yes |
| type  | string | Content template delimiter. The value is always "TomorrowWeather" | Yes |

{% include "./Shared_Weather_Code.md" %}

## Template Example

{% raw %}
```json
{
  "bgClipUrl": {
    "type": "url",
    "value": "https://ssl.pstatic.net/static/clova/service/weather/bg_cloud_daytime.mp4"
  },
  "highTempWeather": {
    "type": "string",
    "value": "구름많음"
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
    "value": "정자1동"
  },
  "lowTempWeather": {
    "type": "string",
    "value": "구름많음"
  },
  "lowTemperature": {
    "type": "temperature-c",
    "value": "23"
  },
  "type": "TomorrowWeather"
}
```
{% endraw %}

## Screen UI example {#UIExample}
The following example shows how the TomorrowWeather template is presented in the Clova mobile app distributed by {{ book.OrientedService }}.
<div class="midAlign"><img style="width: 300px !important" src="/CIC/Resources/Images/Content-Template-TomorrowWeather.png" /></div>

## See also
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)
