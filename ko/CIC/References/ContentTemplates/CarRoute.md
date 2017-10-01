# CarRoute Template
자동차 길찾기 결과 데이터를 제공하는 템플릿입니다. 화면에 자동차 길찾기 결과를 표시할 때 사용됩니다.

<div class="note">
<p><strong>Note!</strong></p>
<p>자동차 길찾기 템플릿을 표시하려면 {{book.OrientedService}} 지도 API에 대한 이해가 필요하며, 템플릿으로 전달된 데이터와 {{book.OrientedService}} 지도 API를 이용하여 길찾기 결과를 지도에 표시해야 합니다. 네이버 지도 API에 대한 자세한 설명은 <a href="https://navermaps.github.io/maps.js/docs/">{{book.OrientedService}} 지도 API 문서</a>를 참고합니다. 길찾기 결과를 표시한 예는 <a href="#UIExample">Screen UI example</a>을 참조합니다.</p>
</div>

## Template field

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `appLinkUrl`                           | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 지도 앱으로 이동하는 URL 정보가 담긴 객체  |
| `boundary`                             | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 전체 보간점을 포함하고 있는 사각의 영역(MBR, Minimum Bounding Rectangle)을 "left,top,right,bottom" 형태의 문자열로 표현한 객체 |
| `linkUrl`                              | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 웹 지도로 이동하는 URL 정보가 담긴 객체   |
| `pathList`                             | [LocationObject](/CIC/References/ContentTemplates/Shared_Objects.md#LocationObject) | 길찾기 경로의 구간점 정보가 있는 객체 배열 |
| `summary`                              | object | 자동차 길찾기 결과의 요약 정보를 담고 있는 객체 |
| `summary.distance`                     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 출발지에서 도착지까지의 이동 거리 정보가 담긴 객체. 단위는 미터(m)입니다. |
| `summary.destination`                  | object | 도착지 정보를 담고 있는 객체 |
| `summary.destination.lat`              | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 도착지의 위도 정보가 담긴 객체 |
| `summary.destination.lon`              | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 도착지의 경도 정보가 담긴 객체 |
| `summary.destination.name`             | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 도착지의 이름 정보가 담긴 객체 |
| `summary.roadSummary[]`                | object array | 길찾기 경로 내 도로 요약 정보를 담고 있는 객체 배열 |
| `summary.roadSummary[].length`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 도로 구간 길이 정보가 담긴 객체. 단위는 미터(m)입니다. |
| `summary.roadSummary[].name`           | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 도로의 이름 정보가 담긴 객체 |
| `summary.roadSummary[].point`          | object | 도로 진입 좌표 정보를 담고 있는 객체 |
| `summary.roadSummary[].point.x`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 네이버 지도에서 도로 진입 지점의 X 좌표 정보를 가진 객체 |
| `summary.roadSummary[].point.y`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 네이버 지도에서 도로 진입 지점의 Y 좌표 정보를 가진 객체 |
| `summary.roadSummary[].roadCongestion` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 도로 상황 정보가 담긴 객체. `summary.roadSummary.roadCongestion.value`는 다음과 같은 값을 가질 수 있습니다. <ul><li><code>"0"</code> : 미수신</li><li><code>"1"</code> : 원활</li><li><code>"2"</code> : 서행</li><li><code>"3"</code> : 지체</li><li><code>"4"</code> : 정체</li></ul> |
| `summary.roadSummary[].speed`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 도로 구간의 평균 속도 정보가 담긴 객체 |
| `summary.start`                        | object | 출발지 정보를 담고 있는 객체 |
| `summary.start.lat`                    | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 출발지의 위도 정보가 담긴 객체 |
| `summary.start.lon`                    | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 출발지의 경도 정보가 담긴 객체 |
| `summary.start.name`                   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 출발지의 이름 정보가 담긴 객체 |
| `summary.time`                         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 예상 이동 시간 정보가 담긴 객체. 단위는 분입니다. |
| `type`                                 | string | Content template 구분자. `"CarRoute"` 값을 가집니다. |

## Template Example

{% raw %}
```json
{
  "type" : "CarRoute",
  "summary" : {
    "distance" : {
      "type" : "string",
      "value" : "62526"
    },
    "time" : {
      "type" : "string",
      "value" : "4526"
    },
    "start" : {
      "lon" : {
        "type" : "string",
        "value" : "349541687"
      },
      "lat" : {
        "type" : "string",
        "value" : "149420527"
      },
      "name" : {
        "type" : "string",
        "value" : "사당역 2호선"
      }
    },
    "destination" : {
      "lon" : {
        "type" : "string",
        "value" : "349541687"
      },
      "lat" : {
        "type" : "string",
        "value" : "149420527"
      },
      "name" : {
        "type" : "string",
        "value" : "사당역 2호선"
      }
    },
    "roadSummary" : [
      {
        "name" : {
          "type" : "string",
          "value" : "과천대로"
        },
        "length" : {
          "type" : "string",
          "value" : "6199"
        },
       "point" : {
         "x" : {
           "type" : "string",
           "value" : "349556545"
         },
         "y" : {
           "type" : "string",
           "value" : "149363287"
         }
       },
       "speed" : {
         "type" : "string",
         "value" : "72"
       },
       "roadCongestion" : {
         "type" : "string",
         "value" : "1"
       }
      }
    ]
  },
  "pathList" : [
    {
      "type" : "location",
      "value" : "349668603.0,149410368.0"
    },
    {
      "type" : "location",
      "value" : "349668603.0,149410368.0"
    }
  ],
  "boundary" : {
    "type" : "string",
    "value" : "349435089,149420518,349561008,149213590"
  },
  "linkUrl" : {
    "type" : "url",
    "value" : "https://..."
  },
  "appLinkUrl" : {
    "type" : "url",
    "value" : "https://..."
  }
}
```
{% endraw %}

## Screen UI example {#UIExample}
다음은 {{ book.OrientedService }}가 배포한 모바일용 Clova 앱에서 CarRoute 템플릿의 내용을 표현한 UI 예제입니다.

![CarRoute](/CIC/Resources/Images/Content-Template-CarRoute.png)

## See also
* [TransportationRoute](/CIC/References/ContentTemplates/TransportationRoute.md)
