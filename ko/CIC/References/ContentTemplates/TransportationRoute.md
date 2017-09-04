# TransportationRoute Template
대중 교통 길찾기 결과 데이터를 제공하는 템플릿입니다. 화면에 대중 교통 길찾기 결과를 표시할 때 사용됩니다. TransportationRoute는 다시 다음과 같은 경로 타입을 가집니다. 각 경로 타입에 따라 `trafficType` 객체의 유효한 필드가 달라질 수 있습니다.

| 구간 타입       | 타입 설명                                           | 유효 필드(`subPath` 객체)       |
|---------------------|---------------------------------------------|-----------------------------|
| 지하철 구간(1)         | 지하철만 이용하는 경로를 표시하는 타입입니다.          | `lane`, `name`, `endID`, `endName`, `endX`, `endY`, `startID`, `startName`, `startX`, `startY`, `subwayCode` |
| 버스 구간(2)          | 버스만 이용하는 경로를 표시하는 타입입니다.            | `busID`, `busNo`, `endID`, `endName`, `endX`, `endY`, `startID`, `startName`, `startX`, `startY`, `type`    |
| 도보 구간(3)          | 지하철과 버스를 복합 이용하는 경로를 표시하는 타입입니다. | `distance`, `sectionTime`                                                                  |

<div class="note">
<p><strong>Note!</strong></p>
<p>대중 교통 길찾기 템플릿을 표시하려면 {{book.OrientedService}} 지도 API에 대한 이해가 필요하며, 템플릿으로 전달된 데이터와 {{book.OrientedService}} 지도 API를 이용하여 길찾기 결과를 지도에 표시해야 합니다. 네이버 지도 API에 대한 자세한 설명은 <a href="https://navermaps.github.io/maps.js/docs/">{{book.OrientedService}} 지도 API 문서</a>를 참고합니다. 길찾기 결과를 표시한 예는 <a href="#UIExample">Screen UI example</a>을 참조합니다.</p>
</div>

## Template field

| 필드 이름       | 자료형    | 필드 설명                     |
|---------------|---------|-----------------------------|
| `appLinkUrl`                | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 지도 앱으로 이동하는 URL 정보가 담긴 객체  |
| `boundary`                  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 전체 보간점을 포함하고 있는 사각의 영역(MBR, Minimum Bounding Rectangle)을 "left,top,right,bottom" 형태의 문자열로 표현한 객체. |
| `busStationCount`           | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 버스로 이동할 때 지나야하는 총 정류장 수 |
| `end`                       | [LocationObject](/CIC/References/ContentTemplates/Shared_Objects.md#LocationObject) | 도착지 좌표 정보가 담긴 객체 |
| `endName`                   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 도착지 이름 정보가 담긴 객체 |
| `linkUrl`                   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | 웹 지도로 이동하는 URL 정보가 담긴 객체   |
| `lanes[]`                   | object array | 길찾기 결과의 모든 경로에 대한 보간점 정보를 가지는 객체 |
| `lanes[].create`            | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 해당 객체의 `section` 필드가 어떤 유형의 정보인지 판단하는 객체. <ul><li><strong>이 필드가 존재하지 않으면</strong> 버스/지하철 구간을 그리는 보간점 정보를 <code>section</code> 필드가 가집니다.</li><li><strong>만약, 이 필드가 존재하고 <code>create.value</code> 값이 <code>"1"</code>이면,</strong> <code>section</code> 필드는 연결선을 그리는 보간점 정보를 가집니다.</ul> |
| `lanes[].section[]`         | [LocationObject](/CIC/References/ContentTemplates/Shared_Objects.md#LocationObject) array | 버스/지하철 구간 또는 구간 사이의 연결선을 그리는 보간점 정보를 가지는 객체 배열. |
| `pathType`                  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 길찾기 결과의 경로 구성 타입을 가지는 객체. `pathType.value` 필드는 다음과 같은 값을 가집니다. <ul><li><code>"1"</code> : 지하철만 이용하는 경로</li><li><code>"2"</code> : 버스만 이용하는 경로</li><li><code>"3"</code> : 지하철과 버스를 복합 이용하는 경로</li></ul>|
| `start`                     | [LocationObject](/CIC/References/ContentTemplates/Shared_Objects.md#LocationObject) | 출발지 좌표 정보가 담긴 객체 |
| `startName`                 | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | 출발지 이름 정보가 담긴 객체 |
| `subPath[]`                 | object array | 각 경로별 세부 구간 정보를 가지는 객체 배열|
| `subPath[].distance`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 특정 구간의 이동 거리 정보가 담긴 객체. 이 필드는 도보 구간(`subPath[].trafficType.value` 필드 값이 `"3"`일 때) 정보를 나타낼 때 사용됩니다. 지하철 또는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"1"`이거나 `"2"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.      |
| `subPath[].endID`           | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 특정 구간에서 하차해야 하는 지하철역/버스 정류장의 ID 정보가 담긴 객체. 이 필드는 지하철 또는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"1"`이거나 `"2"`일 때) 정보를 나타낼 때 사용됩니다. 도보 구간(`subPath[].trafficType.value` 필드 값이 `"3"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].endName`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 특정 구간에서 하차해야 하는 지하철역/버스 정류장의 이름 정보가 담긴 객체. 이 필드는 지하철 또는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"1"`이거나 `"2"`일 때) 정보를 나타낼 때 사용됩니다. 도보 구간(`subPath[].trafficType.value` 필드 값이 `"3"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].endX`            | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 특정 구간에서 하차해야 하는 지하철역/버스 정류장의 X축 좌표 정보가 담긴 객체. 이 필드는 지하철 또는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"1"`이거나 `"2"`일 때) 정보를 나타낼 때 사용됩니다. 도보 구간(`subPath[].trafficType.value` 필드 값이 `"3"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].endY`            | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 특정 구간에서 하차해야 하는 지하철역/버스 정류장의 Y축 좌표 정보가 담긴 객체. 이 필드는 지하철 또는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"1"`이거나 `"2"`일 때) 정보를 나타낼 때 사용됩니다. 도보 구간(`subPath[].trafficType.value` 필드 값이 `"3"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].lane`            | object | 특정 구간에서 이용해야 할 노선 정보가 담긴 객체. 이 필드는 지하철 또는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"1"`이거나 `"2"`일 때) 정보를 나타낼 때 사용됩니다. 도보 구간(`subPath[].trafficType.value` 필드 값이 `"3"`일 때)일 경우 이 필드는 빈 객체일 수도 있습니다. |
| `subPath[].lane.busID`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 버스 ID 정보가 담긴 객체. 이 필드는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"2"`일 때) 정보를 나타낼 때 사용됩니다. 지하철 구간(`subPath[].trafficType.value` 필드 값이 `"1"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].lane.busNo`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 버스 번호 정보가 담긴 객체. 이 필드는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"2"`일 때) 정보를 나타낼 때 사용됩니다. 지하철 구간(`subPath[].trafficType.value` 필드 값이 `"1"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].lane.name`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 지하철 노선 정보가 담긴 객체. 이 필드는 지하철 구간(`subPath[].trafficType.value` 필드 값이 `"1"`일 때) 정보를 나타낼 때 사용됩니다. 버스 구간(`subPath[].trafficType.value` 필드 값이 `"2"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].lane.subwayCode` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | [지하철 코드 정보](#CodeReference)가 담긴 객체. 이 필드는 지하철 구간(`subPath[].trafficType.value` 필드 값이 `"1"`일 때) 정보를 나타낼 때 사용됩니다. 버스 구간(`subPath[].trafficType.value` 필드 값이 `"2"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].lane.type`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | [버스 타입](#CodeReference) 정보가 담긴 객체. 이 필드는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"2"`일 때) 정보를 나타낼 때 사용됩니다. 지하철 구간(`subPath[].trafficType.value` 필드 값이 `"1"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].sectionTime`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 특정 구간의 예상 이동 시간 정보가 담긴 객체. 단위는 분입니다. 이 필드는 도보 구간(`subPath[].trafficType.value` 필드 값이 `"3"`일 때) 정보를 나타낼 때 사용됩니다. 지하철 또는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"1"`이거나 `"2"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다.      |
| `subPath[].startID`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 특정 구간에서 승차해야 하는 지하철역/버스 정류장의 ID 정보가 담긴 객체. 이 필드는 지하철 또는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"1"`이거나 `"2"`일 때) 정보를 나타낼 때 사용됩니다. 도보 구간(`subPath[].trafficType.value` 필드 값이 `"3"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].startName`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 특정 구간에서 승차해야 하는 지하철역/버스 정류장의 이름 정보가 담긴 객체. 이 필드는 지하철 또는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"1"`이거나 `"2"`일 때) 정보를 나타낼 때 사용됩니다. 도보 구간(`subPath[].trafficType.value` 필드 값이 `"3"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].startX`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 특정 구간에서 승차해야 하는 지하철역/버스 정류장의 X축 좌표 정보가 담긴 객체. 이 필드는 지하철 또는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"1"`이거나 `"2"`일 때) 정보를 나타낼 때 사용됩니다. 도보 구간(`subPath[].trafficType.value` 필드 값이 `"3"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].startY`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 특정 구간에서 승차해야 하는 지하철역/버스 정류장의 Y축 좌표 정보가 담긴 객체. 이 필드는 지하철 또는 버스 구간(`subPath[].trafficType.value` 필드 값이 `"1"`이거나 `"2"`일 때) 정보를 나타낼 때 사용됩니다. 도보 구간(`subPath[].trafficType.value` 필드 값이 `"3"`일 때)일 경우 이 객체의 `value` 필드는 빈 문자열(`""`)을 가질 수도 있습니다. |
| `subPath[].trafficType`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 구간 타입. 특정 구간의 이동 수단을 구별하는 식별자입니다. 이 필드 값에 따라 `subPath` 필드의 하위 객체의 구성이 달라질 수 있습니다. 다음과 같은 값을 가질 수 있습니다. <ul><li><code>"1"</code> : 지하철 구간</li><li><code>"2"</code> : 버스 구간</li><li><code>"3"</code> : 도보 구간</li></ul> |
| `SubwayStationCount`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 지하철로 이동할 때 지나야하는 총 지하철역 수 정보가 담긴 객체 |
| `totalDistance`             | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 전체 이동 거리 정보가 담긴 객체. 단위는 미터(m)입니다. |
| `totalStationCount`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 버스 및 지하철로 이동할 때 지나야하는 총 버스 정류장과 지하철역 수의 합 정보가 담긴 객체 |
| `totalTime`                 | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | 전체 예상 이동 시간 정보가 담긴 객체. 단위는 분입니다. |
| `type`                      | string | Content template 구분자. `"TransportationRoute"`로 고정 |


## 지하철 노선 코드 및 버스 타입 코드 {#CodeReference}

| 지하철 노선 코드 | 설명          | 버스 타입 코드   | 설명          |
|--------------|---------------|--------------|--------------|
| 1	           | 수도권_1호선     | 1            | 일반          |
| 2            | 수도권_2호선     | 2            | 좌석          |
| 3            | 수도권_3호선     | 3            | 마을          |
| 4            | 수도권_4호선     | 4            | 직행좌석       |
| 5            | 수도권_5호선     | 5            | 공항          |
| 6            | 수도권_6호선     | 6            | 간선급행       |
| 7            | 수도권_7호선     | 10           | 외곽          |
| 8            | 수도권_8호선     | 11           | 간선          |
| 9            | 수도권_9호선     | 12           | 지선          |
| 21           | 인천_1호선       | 13           | 순환          |
| 31           | 대전_1호선       | 14           | 광역          |
| 41           | 대구_1호선       | 15           | 급행          |
| 42           | 대구_2호선       | 20           | 농어촌        |
| 51           | 광주_1호선       | 21           | 제주시외       |
| 71           | 부산_1호선       | 22           | 시외          |
| 72           | 부산_2호선       | 26           | 급행간선       |
| 73           | 부산_3호선       |              |              |
| 74           | 부산_4호선       |              |              |
| 78           | 부산_동해선       |              |              |
| 79           | 부산_부산김해경전철 |              |              |
| 100          | 분당선           |              |              |
| 101          | 공항철도         |              |              |
| 103          | 중앙선           |              |              |
| 104          | 경의선           |              |              |
| 107          | 에버라인         |              |              |
| 108          | 경춘선           |              |              |
| 109          | 신분당선         |              |              |
| 110          | 의정부경전철      |              |              |
| 111          | 수인선          |              |              |


## Template Example

{% raw %}
```json
{
  "type" : "TransportationRoute",
  "pathType" : {
    "type" : "string",
    "value" : "3"
  },
  "subPath" : [
    {
      "trafficType" : {
        "type" : "string",
        "value" : "3"
      },
      "distance" : {
        "type" : "string",
        "value" : "179"
      },
      "sectionTime" : {
        "type" : "string",
        "value" : "3"
      }
    },
    {
      "trafficType" : {
        "type" : "string",
        "value" : "1"
      },
      "lane" : {
        "name" : {
          "type" : "string",
          "value" : "5호선"
        },
        "subwayCode" : {
          "type" : "string",
          "value" : "5"
        }
      },
      "startX" : {
        "type" : "string",
        "value" : "126.9764454"
      },
      "startY" : {
        "type" : "string",
        "value" : "37.5716197"
      },
      "startID" : {
        "type" : "string",
        "value" : "533"
      },
      "startName" : {
        "type" : "string",
        "value" : "광화문"
      },
      "endX" : {
        "type" : "string",
        "value" : "127.0053025"
      },
      "endY" : {
        "type" : "string",
        "value" : "37.5646938"
      },
      "endID" : {
        "type" : "string",
        "value" : "536"
      },
      "endName" : {
        "type" : "string",
        "value" : "동대문역사문화공원"
      }
    },
    {
      "trafficType" : {
        "type" : "string",
        "value" : "3"
      },
      "distance" : {
        "type" : "string",
        "value" : "26"
      },
      "sectionTime" : {
        "type" : "string",
        "value" : "1"
      }
    },
    {
      "trafficType" : {
        "type" : "string",
        "value" : "2"
      },
      "lane" : {
        "busNo" : {
          "type" : "string",
          "value" : "301"
        },
        "type" : {
          "type" : "string",
          "value" : "11"
        },
        "busID" : {
          "type" : "string",
          "value" : "1006"
        }
      },
      "startX" : {
        "type" : "string",
        "value" : "127.0072774"
      },
      "startY" : {
        "type" : "string",
        "value" : "37.5651429"
      },
      "startID" : {
        "type" : "string",
        "value" : "105343"
      },
      "startName" : {
        "type" : "string",
        "value" : "광희동"
      },
      "endX" : {
        "type" : "string",
        "value" : "127.0611357"
      },
      "endY" : {
        "type" : "string",
        "value" : "37.511781"
      },
      "endID" : {
        "type" : "string",
        "value" : "123460"
      },
      "endName" : {
        "type" : "string",
        "value" : "무역센타"
      }
    },
    {
      "trafficType" : {
        "type" : "string",
        "value" : "3"
      },
      "distance" : {
        "type" : "string",
        "value" : "373"
      },
      "sectionTime" : {
        "type" : "string",
        "value" : "6"
      }
    }
  ],
  "busStationCount" : {
    "type" : "string",
    "value" : "17"
  },
  "subwayStationCount" : {
    "type" : "string",
    "value" : "3"
  },
  "totalStationCount" : {
    "type" : "string",
    "value" : "20"
  },
  "totalTime" : {
    "type" : "string",
    "value" : "55"
  },
  "totalDistance" : {
    "type" : "string",
    "value" : "13284"
  },
  "lanes" : [
    {
      "create" : {
        "type" : "string",
        "value" : "1"
      },
      "section" : [
        {
          "type" : "location",
          "value" : "349538037, 149527412"
        },
        {
          "type" : "location",
          "value" : "349543351, 149521660"
        }
      ]
    },
    {
      "section" : [
        {
          "type" : "location",
          "value" : "349543351, 149521660"
        },
        {
          "type" : "location",
          "value" : "349543376, 149522540"
        },
        {
          "type" : "location",
          "value" : "349543354, 149522879"
        },
        {
          "type" : "location",
          "value" : "349543478, 149524090"
        },
        {
          "type" : "location",
          "value" : "349543584, 149524790"
        }
      ]
    },
    {
      "create" : {
        "type" : "string",
        "value" : "1"
      },
      "section" : [
        {
          "type" : "location",
          "value" : "349600453, 149466463"
        },
        {
          "type" : "location",
          "value" : "349610861, 149458583"
        }
      ]
    }
  ],
  "boundary" : {
    "type" : "string",
    "value" : "349532874,149530952,349610861,149451998"
  },
  "start" : {
    "type" : "location",
    "value" : "349538036,149527412"
  },
  "startName" : {
    "type" : "string",
    "value" : "광화문삼거리"
  },
  "end" : {
    "type" : "location",
    "value" : "349610861,149458582"
  },
  "endName" : {
    "type" : "string",
    "value" : "코엑스"
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
다음은 {{ book.OrientedService }}가 배포한 모바일용 Clova 앱에서 TransportationRoute 템플릿의 내용을 타입별로 표현한 UI 예제입니다.

| 지하철 이용 | 버스 이용 |
|----------|---------|
| ![Subway](/CIC/Resources/Images/Content-Template-TransportationRoute-Use_Only_Subway.png) | ![Bus](/CIC/Resources/Images/Content-Template-TransportationRoute-Use_Only_Bus.png) |

## See also
* [CarRoute](/CIC/References/ContentTemplates/CarRoute.md)
