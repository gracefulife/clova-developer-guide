# CarRoute Template
Provides route directions by driving. It is used to display driving routes on a screen. To display driving routes with this template, you must understand how to use the {{book.OrientedService}} map API. Use data returned from the template together with the {{book.OrientedService}} map API to display directions on a map. See [{{book.OrientedService}} map API documentation](https://navermaps.github.io/maps.js/docs/) for more details on the NAVER map API. See [Screen UI example](#UIExample) for an example of how route directions are displayed.

<div class="note">
<p><strong>Note!</strong></p>
<p>To use the CarRoute template, Prior consultation is necessary with {{ book.OrientedService }}.</p>
</div>


## Template field

| Field name  | Type  | Field description  | Required |
|---------------|---------|-----------------------------|---------|
| appLinkUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | An object that contains a URL which directs users to a map app  | Yes |
| boundary  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object representing a rectangular area (MBR, Minimum Bounding Rectangle) that includes all of interpolated points, in the form of "left,top,right,bottom" string | Yes |
| linkUrl  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)  | An object that contains a URL which directs users to a web map  | Yes |
| pathList  | [LocationObject](/CIC/References/ContentTemplates/Shared_Objects.md#LocationObject) | An object array that contains road segment points along the route | yes |
| summary  | object | An object that contains summary of driving routes | Yes |
| summary.distance  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains a travel distance from a departure point to a destination point. Unit is meter. | Yes |
| summary.destination  | object | An object that contains information on a destination point | Yes |
| summary.destination.lat  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains the latitude of a destination point | Yes |
| summary.destination.lon  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains the longitude of a destination point | Yes |
| summary.destination.name  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains the place name of a destination | Yes |
| summary.roadSummary[]  | object array | An object array that contains summary of roads along the route | Yes |
| summary.roadSummary[].length  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains the length of a road segment. Unit is meter. | Yes |
| summary.roadSummary[].name  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains the name of a road | Yes |
| summary.roadSummary[].point  | object | An object that contains coordinates of a road entry point | Yes |
| summary.roadSummary[].point.x  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains the X coordinate of a road entry point on the NAVER map | Yes |
| summary.roadSummary[].point.y  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains the Y coordinate of a road entry point on the NAVER map | Yes |
| summary.roadSummary[].roadCongestion | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains traffic conditions. *summary.roadSummary.roadCongestion.value* can have the following values. <ul><li>"0": Data was not received</li><li>"1": Free flow of traffic</li><li>"2": Sluggish flow of traffic</li><li>"3": Slow flow of traffic</li><li>"4": Traffic stopped flowing</li></ul> | Yes |
| summary.roadSummary[].speed  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains the average driving speed of a road segment | Yes |
| summary.start  | object | An object that contains information on a departure point | Yes |
| summary.start.lat  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains the latitude of a departure point | Yes |
| summary.start.lon  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains the longitude of a departure point | Yes |
| summary.start.name  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains the place name of a departure point | Yes |
| summary.time  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | An object that contains an estimated travel time. Unit is minute. | Yes |
| type  | string | Content template delimiter. The value is always "CarRoute" | Yes |

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
The following example shows how the CarRoute template is presented in the Clova mobile app distributed by {{ book.OrientedService }}.
<div class="midAlign"><img style="width: 300px !important" src="/CIC/Resources/Images/Content-Template-CarRoute.png" /></div>

## See also
* [TransportationRoute](/CIC/References/ContentTemplates/TransportationRoute.md)
