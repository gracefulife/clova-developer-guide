# Atmosphere Template
Provides atmosphere information. It is used to displays find dust, ultra fine dust, ozone, UV rays and yellow dust on the screen.

<div class="note">
<p><strong>Note!</strong></p>
<p>See <a href="#UIExample">Screen UI example</a> on how atmosphere information are displayed.</p>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `announcementOfAtmosphere`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing forecast guide. This field is eliminated when displaying current atmosphere status. When eliminated, a `value` field of the object will have an empty string (`""`). |
| `bgClipUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object containing a URL of the background video file. <div class="danger"><p><strong>Caution!</strong></p><p>Due to a license issue, this field cannot be used by your partner company. </p></div> |
| `concentrationOfAtmosphere` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing current status or index of atmosphere. This field is eliminated during the forecast. When eliminated, a `value` field of the object will have an empty string (`""`). |
| `halfDayAtmosphereList[]`             | object array | An object array containing atmosphere information in a half day unit (morning/evening).                                    |
| `halfDayAtmosphereList[].atmosphereImageUrl` | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object containing URL of an image file displaying status of atmosphere at the time indicated on `halfDayAtmosphereList[].concentrationOfAtmosphere` field.  |
| `halfDayAtmosphereList[].concentrationOfAtmosphere`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing status of atmosphere or level of air quality at the time indicated on `halfDayAtmosphereList[].concentrationOfAtmosphere` field.   |
| `halfDayAtmosphereList[].durationHalfDay`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing a range of time reflecting atmosphere. In the ‘value’ field of the object, it has `내일 오전`, `내일 오후`, `모레 오전` and `모레 오후` values.  |
| `linkUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | An object containing a link path to the content. The `value` field of this object can have an empty string (`""`).  |
| `location`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing the location. |
| `valueOfAtmosphere`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing current atmosphere index. It includes an index unit. The `value` field of this object can have an empty string (`""`). |
| `type`          | string | A content template delimiter. It has an `"Atmosphere"` value. |

## Template Example

{% raw %}
```json
// Request for current atmosphere information
{
  "announcementOfAtmosphere": {
    "type": "string",
    "value": ""
  },
  "bgClipUrl": {
    "type": "url",
    "value": "https://ssl.pstatic.net/static/clova/service/weather/bg_clean_daytime.mp4"
  },
  "concentrationOfAtmosphere": {
    "type": "string",
    "value": "좋음"
  },
  "failureMessage": {
    "type": "string",
    "value": "경기도 성남시 분당구 정자1동 현재 미세먼지 지수는 좋음 입니다"
  },
  "halfDayAtmosphereList": [
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "보통"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "내일 오전"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "보통"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "내일 오후"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "보통"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "모레 오전"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "보통"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "모레 오후"
      }
    }
  ],
  "location": {
    "type": "string",
    "value": "정자1동"
  },
  "meta": {
    "version": {
      "type": "string",
      "value": "v0.1"
    }
  },
  "type": "Atmosphere",
  "valueOfAtmosphere": {
    "type": "number",
    "value": "27㎍/㎥"
  }
}

// Request for atmosphere of tomorrow
{
  "announcementOfAtmosphere": {
    "type": "string",
    "value": "내일 미세먼지에요"
  },
  "bgClipUrl": {
    "type": "url",
    "value": "https://ssl.pstatic.net/static/clova/service/weather/bg_cloud_daytime.mp4"
  },
  "concentrationOfAtmosphere": {
    "type": "string",
    "value": ""
  },
  "failureMessage": {
    "type": "string",
    "value": "경기도 성남시 분당구 정자1동 내일 미세먼지 지수는 보통 입니다"
  },
  "halfDayAtmosphereList": [
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "보통"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "내일 오전"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "보통"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "내일 오후"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "보통"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "모레 오전"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "보통"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "모레 오후"
      }
    }
  ],
  "location": {
    "type": "string",
    "value": "정자1동"
  },
  "meta": {
    "version": {
      "type": "string",
      "value": "v0.1"
    }
  },
  "type": "Atmosphere",
  "valueOfAtmosphere": {
    "type": "number",
    "value": ""
  }
}
```
{% endraw %}

## Screen UI example {#UIExample}
The following example shows how the Atmosphere template is presented in the Clova mobile app distributed by {{ book.OrientedService }}.

| Current atmosphere status | Atmosphere status of tomorrow |
|-------------|------------|
| ![Now](/CIC/Resources/Images/Content-Template-Atmosphere_Now.png) | ![Original](/CIC/Resources/Images/Content-Template-Atmosphere_Tomorrow.png) |

## See also
* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)
