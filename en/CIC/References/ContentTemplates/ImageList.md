# ImageList template

The ImageList template is used in providing a list of images plus additional information for the client to display on the client's screen.
This template is often used to display a list of thumbnails or the original image.

<div class="note">
<p><strong>Note!</strong></p>
<p>See a <a href="#UIExample">UI example</a> of the ImageList template used in display.</p>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `ImageList[]`                | object array | Contains units of image information.                        |
| `ImageList[].imageReference` | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The name or description of the source of the image. An empty string (`""`) indicates that the source is unavailable.     |
| `ImageList[].imageTitle`     | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The title of the image. An empty string (`""`) indicates that the title is unavailable.           |
| `ImageList[].imageUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The URL of the image. An empty string (`""`) indicates that the image is a thumbnail.      |
| `ImageList[].referenceText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) | The  information on the source of the image. An empty string (`""`) indicates that this information is unavailable.      |
| `ImageList[].referenceURL`   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The URL to the image source. An empty string (`""`) indicates that this information is unavailable.    |
| `ImageList[].thumbImageUrl`  | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)       | The URL of the thumbnail image. An empty string (`""`) indicates that the image is an original image.      |
| `type`                       | string       | The type of this template. The value is always `"ImageList"`.        |

## Template example

{% raw %}
```json
// Example 1.
// User requests for pictures of cars
{
  "type": "ImageList",
  "thumbImageUrlList": [
    {
      "imageReference": {
        "type": "string",
        "value": ""
      },
      "imageTitle": {
        "type": "string",
        "value": "Chauffer at your service as fast as lightning"
      },
      "imageUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m_image&mode=default&query=%EC%9E%90%EB%8F%99%EC%B0%A8%20%EC%9D%B4%EB%AF%B8%EC%A7%80#imgId=post7533909_3"
      },
      "referenceText": {
        "type": "string",
        "value": "NAVER search result"
      },
      "referenceUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%ec%9e%90%eb%8f%99%ec%b0%a8+%ec%82%ac%ec%a7%84+%eb%b3%b4%ec%97%ac%ec%a4%98"
      },
      "thumbImageUrl": {
        "type": "url",
        "value": "https://search.pstatic.net/common/?src=http%3A%2F%2Fpost.phinf.naver.net%2FMjAxNzA1MDZfMTg4%2FMDAxNDk0MDYyNDAwMDY3.C6LJCKXrha2u8dIqOOX0RhQNGrVVfkp3WbLO8U-xzRwg.IEYdykQp6xguEy4bnQ83JhDy1QZOtO4n1Lx5MBwivFwg.JPEG%2FIz2FmvAaRVzSf2Z-sNWzYQVU5z6Q.jpg&type=b360"
      }
    },
    {
      "imageReference": {
        "type": "string",
        "value": ""
      },
      "imageTitle": {
        "type": "string",
        "value": "Car"
      },
      "imageUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m_image&mode=default&query=%EC%9E%90%EB%8F%99%EC%B0%A8%20%EC%9D%B4%EB%AF%B8%EC%A7%80#imgId=gallery2004021016070294818_1"
      },
      "referenceText": {
        "type": "string",
        "value": "NAVER search result"
      },
      "referenceUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%ec%9e%90%eb%8f%99%ec%b0%a8+%ec%82%ac%ec%a7%84+%eb%b3%b4%ec%97%ac%ec%a4%98"
      },
      "thumbImageUrl": {
        "type": "url",
        "value": "https://search.pstatic.net/common/?src=http%3A%2F%2Fthumb.photo.naver.net%2Fdata15%2Fgallery%2F2004-02%2F10%2F07%2F18m2948m0.jpg&type=b360"
      }
    },
    ...
  ]
}

```
{% endraw %}

## UI example {#UIExample}

The following example shows how the ImageList template is used on the Clova app distributed by {{ book.OrientedService }}.

| Thumbnail list | Original image |
|:-------:|:-------:|
| ![Thumbnail](/CIC/Resources/Images/Content_Template-Thumbnail_List.png) | ![Original](/CIC/Resources/Images/Content_Template-Original_Image.png) |

## See also
* [CardList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
* [Popup](/CIC/References/ContentTemplates/Popup.md)
* [Text](/CIC/References/ContentTemplates/Text.md)
