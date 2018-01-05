# ImageText template

The ImageText template is used in providing an image and description for the client to display on the client's screen.

<div class="note">
<p><strong>Note!</strong></p>
<p>See a <a href="#UIExample">UI example</a> of the ImageText template used in display.</p>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `appLinkUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL to the NAVER map app, _if_ the image is an image of a map. An empty string (`""`) indicates that the image is not of a map. |
| `imageUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL of the image. An empty string (`""`) indicates that this information is unavailable.                            |
| `linkUrl`        | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL to a Web map, _if_ the image is an image of a map. An empty string (`""`) indicates that the image is not of a map.   |
| `mainText`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | The text to display on the screen. An empty string (`""`) indicates that text information is unavailable.         |
| `referenceText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | The name or description of the source of the image. An empty string (`""`) indicates that source description is unavailable.             |
| `referenceURL`   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL to the image source. An empty string (`""`) indicates that source URL is unavailable.       |
| `subTextList`    | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | Contains a list of sub-texts. An empty string (`""`) indicates that there is no sub-text to display.      |
| `thumbImageUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL of the thumbnail image. An empty string (`""`) indicates that the image is not a thumbnail image.            |
| `thumbImageType` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | The category of the content of the thumbnail. Available categories are: <ul><li><code>"People"</code>: For people</li><li><code>"Book"</code>: For books</li><li><code>"Album"</code>: For music albums</li><li><code>""</code>(empty string): Category unavailable</li></ul> |
| `type`           | string  | The type of this template. The value is always `"ImageText"` value.      |

## Template example

{% raw %}

```json
// Example 1
// User asks for Lionel Messi's team (A thumbnail image and texts are to be displayed)
{
  "type": "ImageText",
  "imageUrl": {
    "type": "url",
    "value": ""
  },
  "mainText": {
    "type": "string",
    "value": "Lionel Messi"
  },
  "referenceText": {
    "type": "string",
    "value": "NAVER search result"
  },
  "referenceUrl": {
    "type": "url",
    "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%eb%a6%ac%ec%98%a4%eb%84%ac+%eb%a9%94%ec%8b%9c+%ec%86%8c%ec%86%8d%ed%8c%80"
  },
  "subTextList": [
    {
      "type": "string",
      "value": "FC Barcelona"
    }
  ],
  "thumbImageType": {
    "type": "string",
    "value": "People"
  },
  "thumbImageUrl": {
    "type": "url",
    "value": "http://sstatic.naver.net/people/3/201607071816066361.jpg"
  }
}

// Example 2.
// User asks for the current location. An image of a map and descriptions are to be displayed)
{
  "appLinkUrl": {
    "type": "url",
    "value": "nmap://map?lat=37.3594589&lng=127.1047745&level=13&mode=1&traffic=false&bicycle=false&cadastral=false&appname=com.naver.clova"
  },
  "imageUrl": {
    "type": "url",
    "value": "https://simg.pstatic.net/static.map/image?caller=mw_search&crs=EPSG:4326&scale=2&format=jpg&dataversion=163.2&version=1.1&baselayer=default&center=127.1047745,37.3594589&markers=type,default2_s,127.1047745,37.3594589&level=10&h=402&w=515"
  },
  "linkUrl": {
    "type": "url",
    "value": "https://m.map.naver.com/map.nhn?lat=37.3594589&lng=127.1047745&dlevel=&mapMode=&pinTitle=&boundary=&traffic="
  },
  "mainText": {
    "type": "string",
    "value": "Tokyo, Shinjuku-ku, Shinjuku"
  },
  "meta": {
    "version": {
      "type": "string",
      "value": "v0.1"
    }
  },
  "referenceText": {
    "type": "string",
    "value": "NAVER search result"
  },
  "referenceUrl": {
    "type": "url",
    "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%ed%98%84%ec%9e%ac+%ec%9c%84%ec%b9%98"
  },
  "subTextList": [
    {
      "type": "string",
      "value": ""
    }
  ],
  "thumbImageType": {
    "type": "string",
    "value": ""
  },
  "thumbImageUrl": {
    "type": "url",
    "value": ""
  },
  "type": "ImageText"
}
```

{% endraw %}

## UI example {#UIExample}

The following example shows how the ImageText template is used on the Clova app distributed by {{ book.OrientedService }}.

| Thumbnail image with text | Map image with text |
|:-------:|:-------:|
| ![Thumbnail](/CIC/Resources/Images/Content_Template-Thumbimage_and_Text.png) | ![Map and text](/CIC/Resources/Images/Content_Template-Mapimage_and_Text.png) |

## See also
* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [Popup](/CIC/References/ContentTemplates/Popup.md)
* [Text](/CIC/References/ContentTemplates/Text.md)
