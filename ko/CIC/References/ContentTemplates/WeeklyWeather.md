# WeeklyWeather Template
주간 날씨 정보를 제공하는 템플릿입니다. 화면에 주간 날씨 정보를 표시할 때 사용됩니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>주간 날씨 정보를 표시한 예는 <a href="#UIExample">UI example</a>을 참조합니다.</p>
</div>

## Template fields

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `bgClipUrl`                       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 배경 영상 파일의 URL 정보가 담긴 객체. <div class="danger"><p><strong>Caution!</strong></p><p>해당 필드의 데이터는 라이센스 문제로 제휴처에서는 사용하실 수 없습니다.</p></div> |
| `dailyWeatherList[]`              | object array | 일일 날씨 정보를 가지는 객체 배열 |
| `dailyWeatherList[].date`         | [DateObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateObject) | 날짜 정보를 가진 객체 |
| `dailyWeatherList[].highTemperature` | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | 해당 날짜의 최고 기온 정보가 담긴 객체 |
| `dailyWeatherList[].iconImageCode` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 날짜별 [날씨 코드](#WeatherCode) 정보가 담긴 객체 |
| `dailyWeatherList[].iconImageUrl` | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 해당 날짜의 날씨 정보를 표현하는 이미지 아이콘의 URL 정보를 가지는 객체 |
| `dailyWeatherList[].lowTemperature`  | [TemperatureCObject](/CIC/References/ContentTemplates/Shared_Objects.md#TemperatureCObject) | 해당 날짜의 최저 기온 정보가 담긴 객체 |
| `description`               | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 주간 날씨 정보임을 알리는 설명 문구가 포함된 객체  |
| `linkUrl`                   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 콘텐츠 링크 경로가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.   |
| `location`                  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 지역 정보가 담긴 객체 |
| `type`                      | string | Content template 구분자. `"WeeklyWeather"` 값을 가집니다. |

{% include "./Shared_Weather_Code.md" %}

## Template example

{% raw %}
```json
{
  "bgImageUrl": {
    "type": "url",
    "value": "https://ssl.pstatic.net/static/clova/service/weather/bg_cloud_daytime.mp4"
  },
  "dailyWeatherList": [
    {
      "date": {
        "type": "date",
        "value": "20170726"
      },
      "highTemperature": {
        "type": "temperature-c",
        "value": "33"
      },
      "iconImageCode": {
        "type": "string",
        "value": "3"
      },
      "iconImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_03.png"
      },
      "lowTemperature": {
        "type": "temperature-c",
        "value": "23"
      }
    },
    {
      "date": {
        "type": "date",
        "value": "20170727"
      },
      "highTemperature": {
        "type": "temperature-c",
        "value": "32"
      },
      "iconImageCode": {
        "type": "string",
        "value": "5"
      },
      "iconImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      },
      "lowTemperature": {
        "type": "temperature-c",
        "value": "23"
      }
    },
    {
      "date": {
        "type": "date",
        "value": "20170728"
      },
      "highTemperature": {
        "type": "temperature-c",
        "value": "31"
      },
      "iconImageCode": {
        "type": "string",
        "value": "9"
      },
      "iconImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_09.png"
      },
      "lowTemperature": {
        "type": "temperature-c",
        "value": "24"
      }
    },
    {
      "date": {
        "type": "date",
        "value": "20170729"
      },
      "highTemperature": {
        "type": "temperature-c",
        "value": "29"
      },
      "iconImageCode": {
        "type": "string",
        "value": "22"
      },
      "iconImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_22.png"
      },
      "lowTemperature": {
        "type": "temperature-c",
        "value": "24"
      }
    },
    {
      "date": {
        "type": "date",
        "value": "20170730"
      },
      "highTemperature": {
        "type": "temperature-c",
        "value": "29"
      },
      "iconImageCode": {
        "type": "string",
        "value": "5"
      },
      "iconImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      },
      "lowTemperature": {
        "type": "temperature-c",
        "value": "23"
      }
    },
    {
      "date": {
        "type": "date",
        "value": "20170731"
      },
      "highTemperature": {
        "type": "temperature-c",
        "value": "29"
      },
      "iconImageCode": {
        "type": "string",
        "value": "5"
      },
      "iconImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      },
      "lowTemperature": {
        "type": "temperature-c",
        "value": "23"
      }
    },
    {
      "date": {
        "type": "date",
        "value": "20170801"
      },
      "highTemperature": {
        "type": "temperature-c",
        "value": "30"
      },
      "iconImageCode": {
        "type": "string",
        "value": "5"
      },
      "iconImageUrl": {
        "type": "url",
        "value": "https://ssl.pstatic.net/static/clova/service/weather/icon_05.png"
      },
      "lowTemperature": {
        "type": "temperature-c",
        "value": "22"
      }
    }
  ],
  "description": {
    "type": "string",
    "value": "주간 날씨예요"
  },
  "location": {
    "type": "string",
    "value": "정자1동"
  },
  "type": "WeeklyWeather"
}
```
{% endraw %}

## UI example {#UIExample}
다음은 {{ book.OrientedService }}가 배포한 모바일용 Clova 앱에서 WeeklyWeather 템플릿의 내용을 표현한 UI 예제입니다.

![WeeklyWeather](/CIC/Resources/Images/Content-Template-WeeklyWeather.png)

## See also
* [Atmosphere](/CIC/References/ContentTemplates/Atmosphere.md)
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)
