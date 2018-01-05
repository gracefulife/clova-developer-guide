# Atmosphere Template

The Atmosphere template is used in providing atmosphere information for the client to display on the client's screen.
The type of atmosphere information provided includes information on fine dust, ultra-fine dust, ozone, UV rays and yellow dust.

<div class="note">
<p><strong>Note!</strong></p>
<p>See a <a href="#UIExample">UI example</a> for the Atmosphere template used in display.</p>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `announcementOfAtmosphere`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | Contains a statement on the forecast. An empty string (`""`) indicates that the information received contains the current atmosphere information, not a forecast. |
| `bgClipUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | The URL of the video file to play in the background.<div class="danger"><p><strong>Caution!</strong></p><p>Due to a license issue, you are not permitted to use this URL.</p></div> |
| `concentrationOfAtmosphere` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The _current_ level of air quality. An empty string (`""`) indicates that the information received contains forecasts, not the current information. |
| `halfDayAtmosphereList[]`             | object array | Contains multiple atmosphere information blocks in half day (morning/afternoon) units.                                   |
| `halfDayAtmosphereList[].atmosphereImageUrl` | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | The link to the image associated with the atmosphere information specified by the `halfDayAtmosphereList[].durationHalfDay` field. |
| `halfDayAtmosphereList[].concentrationOfAtmosphere`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The level of air quality for the time specified by the `halfDayAtmosphereList[].durationHalfDay` field.   |
| `halfDayAtmosphereList[].durationHalfDay`   | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The time scope the associated atmosphere information is for. Available values are:<ul><li><code>Tomorrow morning</code></li><li><code>Tomorrow afternoon</code></li><li><code>The day after tomorrow's morning</code></li><li><code>The day after tomorrow's afternoon</code></li></ul>  |
| `linkUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject) | The link to the content to display when the air quality information is tapped by the user. An empty string (`""`) indicates that no content is to be displayed.  |
| `location`      | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The location which the atmosphere information is for. |
| `valueOfAtmosphere`         | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The current air quality index, with the index unit. An empty string (`""`) indicates that this information is unavailable. |
| `type`          | string | The type of this template. The value is always `"Atmosphere"`. |

## Template example

{% raw %}
```json
// Current atmosphere information
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
    "value": "Good"
  },
  "failureMessage": {
    "type": "string",
    "value": "The current fine dust level for Shinjuku is good"
  },
  "halfDayAtmosphereList": [
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "Moderate"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "Tomorrow morning"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "Moderate"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "Tomorrow afternoon"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "Moderate"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "The day after tomorrow's morning"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "Moderate"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "The day after tomorrow's afternoon"
      }
    }
  ],
  "location": {
    "type": "string",
    "value": "Shinjuku"
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

// Atmosphere information for tomorrow
{
  "announcementOfAtmosphere": {
    "type": "string",
    "value": "Here is tomorrow's fine dust level"
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
    "value": "Tomorrow's fine dust level is moderate for Shinjuku"
  },
  "halfDayAtmosphereList": [
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "Normal"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "Tomorrow morning"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "Normal"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "Tomorrow afternoon"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "Normal"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "The day after tomorrow's morning"
      }
    },
    {
      "atmosphereImageUrl": {
        "type": "url",
        "value": "http://static.naver.net/clova/service/weather/air_icon_02.png"
      },
      "concentrationOfAtmosphere": {
        "type": "string",
        "value": "Normal"
      },
      "durationHalfDay": {
        "type": "string",
        "value": "The day after tomorrow's afternoon"
      }
    }
  ],
  "location": {
    "type": "string",
    "value": "Shinjuku"
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

## UI example {#UIExample}

The following examples show how the Atmosphere template is used on the Clova app distributed by {{ book.OrientedService }}.

| Current atmosphere status | Atmosphere status for tomorrow |
|:-------------:|:------------:|
| ![Now](/CIC/Resources/Images/Content-Template-Atmosphere_Now.png) | ![Original](/CIC/Resources/Images/Content-Template-Atmosphere_Tomorrow.png) |

## See also

* [Humidity](/CIC/References/ContentTemplates/Humidity.md)
* [TodayWeather](/CIC/References/ContentTemplates/TodayWeather.md)
* [TomorrowWeather](/CIC/References/ContentTemplates/TomorrowWeather.md)
* [WeeklyWeather](/CIC/References/ContentTemplates/WeeklyWeather.md)
* [WindSpeed](/CIC/References/ContentTemplates/WindSpeed.md)
