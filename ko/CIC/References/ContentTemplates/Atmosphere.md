# Atmosphere Template
대기 정보를 제공하는 템플릿입니다. 화면에 미세먼지, 초미세먼지, 오존, 자외선, 황사 정보를 표시할 때 사용됩니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>대기 정보를 표시한 예는 <a href="#UIExample">Screen UI example</a>을 참조합니다.</p>
</div>

## Template field

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `announcementOfAtmosphere`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 예보 안내 문구가 담긴 객체. 현재 대기 상태 정보를 보여줄 때는 이 필드가 생략됩니다. 생략될 때 이 객체의 `value` 필드는 빈 문자열(`""`)을 가집니다. |
| `bgClipUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 배경 영상 파일의 URL 정보가 담긴 객체. <div class="danger"><p><strong>Caution!</strong></p><p>해당 필드의 데이터는 라이센스 문제로 제휴처에서는 사용하실 수 없습니다.</p></div> |
| `concentrationOfAtmosphere` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 현재 대기 상태나 지수 정보가 담긴 객체. 예보를 할 때는 이 필드가 생략됩니다. 생략될 때는 이 객체의 `value` 필드는 빈 문자열(`""`)을 가집니다. |
| `halfDayAtmosphereList[]`             | object array | 반나절 단위(오전/오후)로 구분된 시간대별 대기 정보를 가지는 객체 배열                                    |
| `halfDayAtmosphereList[].atmosphereImageUrl` | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 해당 시간대의 대기 상태를 표시하는 이미지 파일의 URL 정보가 담긴 객체 |
| `halfDayAtmosphereList[].concentrationOfAtmosphere`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 해당 시간대의 대기 상태나 지수 정보가 담긴 객체.  |
| `halfDayAtmosphereList[].durationHalfDay`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 시간대 정보가 담긴 객체. 이 객체의 `value` 필드는 `내일 오전`, `내일 오후`, `모레 오전`, `모레 오후`와 같은 값을 가집니다.  |
| `linkUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | 콘텐츠 링크 경로가 담긴 객체. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.  |
| `location`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 지역 정보가 담긴 객체 |
| `valueOfAtmosphere`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 현재 대기의 수치 정보가 담긴 객체. 수치의 단위가 포함되어 있습니다. 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `type`          | string | Content template 구분자. `"Atmosphere"`로 고정 |

## Template Example

{% raw %}
```json
// 현재 대기 정보 요청
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

// 내일 대기 정보 요청
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
다음은 {{ book.OrientedService }}가 배포한 모바일용 Clova 앱에서 Atmosphere 템플릿의 내용을 표현한 UI 예제입니다.

| 현재 대기 상태 | 내일 대기 상태 |
|-------------|------------|
| ![Now](/CIC/Resources/Images/Content-Template-Atmosphere_Now.png) | ![Original](/CIC/Resources/Images/Content-Template-Atmosphere_Tomorrow.png) |

## See also
* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)
