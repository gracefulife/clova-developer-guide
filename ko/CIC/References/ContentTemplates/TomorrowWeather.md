# TomorrowWeather Template
내일 날씨 정보를 제공하는 템플릿입니다. 화면에 내일 날씨 정보를 표시할 때 사용됩니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>내일 날씨 정보를 표시한 예는 <a href="#UIExample">Screen UI example</a>을 참조합니다.</p>
</div>

## Template field

| 필드 이름       | 자료형    | 필드 설명                     | 필수 여부 |
|---------------|---------|-----------------------------|---------|
| `bgClipUrl`                 | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 배경음 파일의 URL 정보가 담긴 객체 | 필수 |
| `highTemperature`           | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | 내일 오후의 최고 기온 정보가 담긴 객체 | 필수 |
| `highTempWeather`           | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 기온이 가장 높을 때의 날씨 정보가 담긴 객체  | 필수 |
| `houlyWeatherList[]` | object array | 시간대별 날씨 정보를 가지는 객체 배열 | 필수 |
| `houlyWeatherList[].hourlyTemperature` | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | 시간대별 온도 정보가 담긴 객체 | 필수 |
| `houlyWeatherList[].hourlyTime` | [DateTimeObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateTimeObject) | 시간대 정보가 담긴 객체 | 필수 |
| `houlyWeatherList[].rainfallProbability` | [PercentageObject](/CIC/References/ContentTemplates/Shared_Objects.md#PercentageObject) | 강수 확률 정보가 담긴 객체 | 선택 |
| `houlyWeatherList[].temperatureImageCode` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 시간대별 [날씨 코드](#WeatherCode) 정보가 담긴 객체 | 필수 |
| `houlyWeatherList[].temperatureImageUrl` | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 시간대별 날씨 이미지 파일의 URL 정보가 담긴 객체 | 필수 |
| `linkUrl`                   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 콘텐츠 링크 경로가 담긴 객체   | 선택 |
| `location`                  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 지역 정보가 담긴 객체 | 필수 |
| `lowTemperature`           | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | 내일 오전의 최저 기온 정보가 담긴 객체 | 필수 |
| `lowTempWeather`           | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 기온이 가장 낮을 때의 날씨 정보가 담긴 객체  | 필수 |
| `type`                      | string | Content template 구분자. `"TomorrowWeather"`로 고정 | 필수 |

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
다음은 {{ book.OrientedService }}가 배포한 모바일용 Clova 앱에서 TomorrowWeather 템플릿의 내용을 표현한 UI 예제입니다.

![TomorrowWeather](/CIC/Resources/Images/Content-Template-TomorrowWeather.png)

## See also
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)