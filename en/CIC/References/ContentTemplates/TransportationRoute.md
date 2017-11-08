# TransportationRoute template
Provides route directions for public transportations. It is used to display public transportation routes on a screen. TransportationRoute has routes types as follows. For each route type, valid fields for the `trafficType` object can vary.

| Section type       | Type description                                           | Valid fields (`subPath` object)       |
|---------------------|---------------------------------------------|-----------------------------|
| Subway section(1)         | Displays routes that use subways only.          | `lane`, `name`, `endID`, `endName`, `endX`, `endY`, `startID`, `startName`, `startX`, `startY`, `subwayCode` |
| Bus section(2)          | Displays routes that use buses only.            | `busID`, `busNo`, `endID`, `endName`, `endX`, `endY`, `startID`, `startName`, `startX`, `startY`, `type`    |
| Walking section(3)          | Displays routes that use both subways and buses. | `distance`, `sectionTime`                                                                  |

<div class="note">
<p><strong>Note!</strong></p>
<p>To display public transportation routes with this template, you must understand how to use the {{book.OrientedService}} map API. Use data returned from the template with the {{book.OrientedService}} map API to display directions on a map. See <a href="https://navermaps.github.io/maps.js/docs/">{{book.OrientedService}} map API documentation</a> for more details on the NAVER map API. See <a href="#UIExample">Screen UI example</a> on how route directions are displayed.</p>
</div>

## Template field

| Field name       | Type    | Field description                     |
|---------------|---------|-----------------------------|
| `appLinkUrl`                | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | An object containing a URL which redirects to a map app  |
| `boundary`                  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object representing a rectangular area (MBR, Minimum Bounding Rectangle) that includes all of interpolated points, in the form of "left,top,right,bottom" string. |
| `busStationCount`           | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The total number of stops to pass through when traveling by bus |
| `end`                       | [LocationObject](/CIC/References/ContentTemplates/Shared_Objects.md#LocationObject) | An object containing coordinates of the destination point |
| `endName`                   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing the name of the destination point |
| `linkUrl`                   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | An object containing a URL which redirects to a web map   |
| `lanes[]`                   | object array | An object containing interpolated points on all routes found |
| `lanes[].create`            | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that decides the `section` type of the object. <ul><li><strong>If this field does not exist,</strong> the <code>section</code> field contains interpolated points for drawing bus/subway sections.</li><li><strong>If this field does exist and <code>create.value</code> is set to <code>"1"</code>,</strong> the <code>section</code> field contains interpolated points for drawing polylines.</ul> |
| `lanes[].section[]`         | [LocationObject](/CIC/References/ContentTemplates/Shared_Objects.md#LocationObject) array | An object array containing interpolated points for drawing bus/subway sections or polylines between sections. |
| `pathType`                  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing the route type of the direction. The `pathType.value` field has the following values. <ul><li><code>"1"</code>: Routes that use subways only</li><li><code>"2"</code>: Routes that use buses only</li><li><code>"3"</code>: Routes that use both subways and buses</li></ul>|
| `start`                     | [LocationObject](/CIC/References/ContentTemplates/Shared_Objects.md#LocationObject) | An object containing coordinates of the departure point |
| `startName`                 | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)     | An object containing the name of the departure point |
| `subPath[]`                 | object array | An object array containing details of sections on each route |
| `subPath[].distance`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing a travel distance of a given section. This field is used to show walking section details (`subPath[].trafficType.value` is `"3"`). When it is a subway or bus section (`subPath[].trafficType.value` is `"1"` or `"2"`), the `value` field of this object can have an empty string (`""`).      |
| `subPath[].endID`           | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing IDs of subway stations/bus stops to get off in a given section. This field is used to show subway or bus section details (`subPath[].trafficType.value` is `"1"` or `"2"`). When it is a walking section (`subPath[].trafficType.value` is `"3"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].endName`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing names of subway stations/bus stops to get off in a given section. This field is used to show subway or bus section details (`subPath[].trafficType.value` is `"1"` or `"2"`). When it is a walking section (`subPath[].trafficType.value` is `"3"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].endX`            | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing X coordinates of subway stations/bus stops to get off in a given section. This field is used to show subway or bus section details (`subPath[].trafficType.value` is `"1"` or `"2"`). When it is a walking section (`subPath[].trafficType.value` is `"3"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].endY`            | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing Y coordinates of subway stations/bus stops to get off in a given section. This field is used to show subway or bus section details (`subPath[].trafficType.value` is `"1"` or `"2"`). When it is a walking section (`subPath[].trafficType.value` is `"3"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].lane`            | object | An object containing details of lanes in a given section. This field is used to show subway or bus section details (`subPath[].trafficType.value` is `"1"` or `"2"`). When it is a walking section (`subPath[].trafficType.value` is `"3"`), this field can be an empty object. |
| `subPath[].lane.busID`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing bus IDs. This field is used to show bus section details (`subPath[].trafficType.value` is `"2"`). When it is a subway section (`subPath[].trafficType.value` is `"1"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].lane.busNo`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing bus numbers. This field is used to show bus section details (`subPath[].trafficType.value` is `"2"`). When it is a subway section (`subPath[].trafficType.value` is `"1"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].lane.name`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing subway lanes. This field is used to show subway section details (`subPath[].trafficType.value` is `"1"`). When it is a bus section (`subPath[].trafficType.value` is `"2"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].lane.subwayCode` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing [subway codes](#CodeReference). This field is used to show subway section details (`subPath[].trafficType.value` is `"1"`). When it is a bus section (`subPath[].trafficType.value` is `"2"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].lane.type`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing [bus types](#CodeReference). This field is used to show bus section details (`subPath[].trafficType.value` is `"2"`). When it is a subway section (`subPath[].trafficType.value` is `"1"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].sectionTime`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing an estimated travel time at a given section. Unit is minute. This field is used to show walking section details (`subPath[].trafficType.value` is `"3"`). When it is a subway or bus section (`subPath[].trafficType.value` is `"1"` or `"2"`), the `value` field of this object can have an empty string (`""`).      |
| `subPath[].startID`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing IDs of subway stations/bus stops to get on in a given section. This field is used to show subway or bus section details (`subPath[].trafficType.value` is `"1"` or `"2"`). When it is a walking section (`subPath[].trafficType.value` is `"3"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].startName`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing names of subway stations/bus stops to get on in a given section. This field is used to show subway or bus section details (`subPath[].trafficType.value` is `"1"` or `"2"`). When it is a walking section (`subPath[].trafficType.value` is `"3"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].startX`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing X coordinates of subway stations/bus stops to get on in a given section. This field is used to show subway or bus section details (`subPath[].trafficType.value` is `"1"` or `"2"`). When it is a walking section (`subPath[].trafficType.value` is `"3"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].startY`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing Y coordinates of subway stations/bus stops to get on in a given section. This field is used to show subway or bus section details (`subPath[].trafficType.value` is `"1"` or `"2"`). When it is a walking section (`subPath[].trafficType.value` is `"3"`), the `value` field of this object can have an empty string (`""`). |
| `subPath[].trafficType`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Section type. It is an identifier for distinguishing travel methods at a given section. Depending on the value of this field, configuration of sub objects in the `subPath` field can vary. Available values are: <ul><li><code>"1"</code>: Subway section</li><li><code>"2"</code>: Bus section</li><li><code>"3"</code>: Walking section</li></ul> |
| `SubwayStationCount`        | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing the total number of subway stations to pass through when traveling by subway |
| `totalDistance`             | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing a total travel distance. Unit is meter. |
| `totalStationCount`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing the total number of bus stops and subway stations to pass through when traveling by bus and subway |
| `totalTime`                 | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object containing an estimated total travle time. Unit is minute. |
| `type`                      | string | A content template delimiter. It has an `"TransportationRoute"` value. |


## Codes for subway lines and bus types {#CodeReference}

| Subway line code | Description          | But type code   | Description          |
|--------------|---------------|--------------|--------------|
| 1	           | Metropolitan_Line 1     | 1            | Regular          |
| 2            | Metropolitan_Line 2     | 2            | Seats          |
| 3            | Metropolitan_Line 3     | 3            | Town          |
| 4            | Metropolitan_Line 4     | 4            | Express seats       |
| 5            | Metropolitan_Line 5     | 5            | Airport          |
| 6            | Metropolitan_Line 6     | 6            | Main roads direct express       |
| 7            | Metropolitan_Line 7     | 10           | Suburb          |
| 8            | Metropolitan_Line 8     | 11           | Main roads          |
| 9            | Metropolitan_Line 9     | 12           | Local lines          |
| 21           | Incheon_Line 1       | 13           | Circular          |
| 31           | Daejeon_Line 1       | 14           | Metropolitan          |
| 41           | Daegu_Line 1       | 15           | Direct express          |
| 42           | Daegu_Line 2       | 20           | Rural region        |
| 51           | Gwangju_Line 1       | 21           | Jeju region       |
| 71           | Busan_Line 1       | 22           | Countryside          |
| 72           | Busan_Line 2       | 26           | Direct express main road       |
| 73           | Busan_Line 3       |              |              |
| 74           | Busan_Line 4       |              |              |
| 78           | Busan_East Sea Line       |              |              |
| 79           | Busan_Gimhae Light Rail Transit |              |              |
| 100          | Bundang Line           |              |              |
| 101          | Airport Railroad         |              |              |
| 103          | Jungang Line           |              |              |
| 104          | Gyeongui Line           |              |              |
| 107          | Everline         |              |              |
| 108          | Gyeongchun Line           |              |              |
| 109          | Sinbundang Line         |              |              |
| 110          | U Line      |              |              |
| 111          | Suin Line          |              |              |


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
The following example shows how the TransportationRoute template is presented for each type in the Clova mobile app distributed by {{ book.OrientedService }}.

| Using subway | Using bus |
|----------|---------|
| ![Subway](/CIC/Resources/Images/Content-Template-TransportationRoute-Use_Only_Subway.png) | ![Bus](/CIC/Resources/Images/Content-Template-TransportationRoute-Use_Only_Bus.png) |

## See also
* [CarRoute](/CIC/References/ContentTemplates/CarRoute.md)