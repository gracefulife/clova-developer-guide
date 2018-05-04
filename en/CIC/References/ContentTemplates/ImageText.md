# ImageText Template
The ImageText template is used in providing an image and description for the client to display on the client screen. This template is used when displaying thumbnail image and text or when displaying a map and text together.

<div class="note">
<p><strong>Note!</strong></p>
<p>See a <a href="#UIExample">UI example</a> of the ImageText template used in display.</p>
</div>

## Template fields

| Field name       | Data type    | Description                     |
|---------------|---------|-----------------------------|
| `appLinkUrl`     | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL to the {{ book.OrientedService }} map app, if a map image is included. An empty string (`""`) indicates that no content is to be displayed.  |
| `imageUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL of the image. An empty string (`""`) indicates that no content is to be displayed.                                |
| `linkUrl`        | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL to a web map, if a map image is included. An empty string (`""`) indicates that no content is to be displayed.   |
| `mainText`       | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | The main text to display. An empty string (`""`) indicates that no content is to be displayed.                                       |
| `referenceText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | The information of the referred service. An empty string (`""`) indicates that no content is to be displayed.  |
| `referenceUrl`   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The information on the usage result URL of the referred service. An empty string (`""`) indicates that no content is to be displayed.   |
| `subTextList[]`    | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | The object array that has the sub-texts. An empty string (`""`) indicates that no content is to be displayed.                               |
| `thumbImageUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL of the thumbnail image. An empty string (`""`) indicates that no content is to be displayed.                           |
| `thumbImageType` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | The category of thumbnail content. <ul><li><code>"People"</code>: On people</li><li><code>"Book"</code>: On book information</li><li><code>"Album"</code>: On music albums</li><li>Empty string(<code>""</code>): No thumbnail information</li></ul> |
| `type`           | string  | The type of this template. The value is always `"ImageText"`.      |

## Template example

{% raw %}

```json
// Example 1.
// User request: What is the name of Lionel Messi's team? (A thumbnail image and text are to be displayed)
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
    "value": "https://m.search.contentproviderdomain.com/search?where=m&sm=mob_lic&query=%eb%a6%ac%ec%98%a4%eb%84%ac+%eb%a9%94%ec%8b%9c+%ec%86%8c%ec%86%8d%ed%8c%80"
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
    "value": "http://sstatic.contentproviderdomain.net/people/3/201607071816066361.jpg"
  }
}

// Example 2.
// User request: Where am I? (An image of a map and descriptions are to be displayed)
{
  "appLinkUrl": {
    "type": "url",
    "value": "nmap://map?lat=37.3594589&lng=127.1047745&level=13&mode=1&traffic=false&bicycle=false&cadastral=false&appname=com.contentproviderdomain.clova"
  },
  "imageUrl": {
    "type": "url",
    "value": "https://simg.pstatic.net/static.map/image?caller=mw_search&crs=EPSG:4326&scale=2&format=jpg&dataversion=163.2&version=1.1&baselayer=default&center=127.1047745,37.3594589&markers=type,default2_s,127.1047745,37.3594589&level=10&h=402&w=515"
  },
  "linkUrl": {
    "type": "url",
    "value": "https://m.map.contentproviderdomain.com/map.nhn?lat=37.3594589&lng=127.1047745&dlevel=&mapMode=&pinTitle=&boundary=&traffic="
  },
  "mainText": {
    "type": "string",
    "value": "Shinjuku"
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
    "value": "https://m.search.contentproviderdomain.com/search?where=m&sm=mob_lic&query=%ed%98%84%ec%9e%ac+%ec%9c%84%ec%b9%98"
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

| Thumbnail image and text | Map image and text |
|-------|-------|
| ![Thumbnail](/CIC/Resources/Images/Content_Template-Thumbimage_and_Text.png) | ![Map and text](/CIC/Resources/Images/Content_Template-Mapimage_and_Text.png) |

## See also
* [CardList](/CIC/References/ContentTemplates/CardList.md)
* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [Popup](/CIC/References/ContentTemplates/Popup.md)
* [Text](/CIC/References/ContentTemplates/Text.md)
