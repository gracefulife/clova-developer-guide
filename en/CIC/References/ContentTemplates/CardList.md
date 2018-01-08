# CardList template

The CardList template is used in providing multimedia information for the client to display on the client's screen.
The CardList template provides different card types for different media type.
For each card type, valid fields of a card object (an element of the `cardList[]` array) vary as shown in the table below:

| Card type       | Description                      | Valid fields        |
|---------------|-----------------------------|-----------------------------|
| `Type1` | Card to display an image, title, and description        | `description`, `imageUrl`, `referenceText`, `referenceUrl`, `title`               |
| `Type2` | Card to display an image, title, description, and link  | `description`, `imageUrl`, `linkUrl`, `referenceText`, `referenceUrl`, `title`    |
| `Type3` | Card to display a video                                 | `description`, `imageUrl`, `referenceText`, `referenceUrl`, `title`, `videoUrl`   |
| `Type4` | Card to display news                                    | `description`, `press`, `pressIconUrl`, `publishDate`, `title`                    |
| `Type5` | Card to display audio information                           | `description`, `imageUrl`, `title`, `videoUrl`                                    |
| `Type6` | Card to display a media thumbnail                       | `imageUrl`, `linkUrl`                                                             |

<div class="note">
<p><strong>Note!</strong></p>
<p>See a <a href="#UIExample">UI example</a> for each card type in display.</p>
</div>

## Template fields

| Field name       | Type    | Description                     |
|---------------|---------|-----------------------------|
| `cardList[]`                | object array | Contains a list of information units to be displayed as cards. |
| `cardList[].description[]`    | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject) array | Contains information about the content this card is to display. |
| `cardList[].imageUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL of the image to display. An empty string (`""`) indicates that this information is unavailable for this card. |
| `cardList[].linkUrl`        | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL of the content. An empty string (`""`) indicates that this information is unavailable for this card.         |
| `cardList[].press`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | The name of the press for news. An empty string (`""`) indicates that this information is unavailable for this card.             |
| `cardList[].pressIconUrl`   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL to the press icon for news. An empty string (`""`) indicates that this information is unavailable for this card.    |
| `cardList[].publishDate`    | [DateObject](/CIC/References/ContentTemplates/Shared_Objects.md#DateObject)           | The published date of the associated article. An empty string (`""`) indicates that this information is unavailable for this card.            |
| `cardList[].referenceText`  | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | The name or description of the content source. An empty string (`""`) indicates that this information is unavailable for this card.         |
| `cardList[].referenceURL`   | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL of the content source. An empty string (`""`) indicates that this information is unavailable for this card.          |
| `cardList[].title`          | [StringObject](/CIC/References/ContentTemplates/Shared_Objects.md#StringObject)       | The title of the content.             |
| `cardList[].videoUrl`       | [URLObject](/CIC/References/ContentTemplates/Shared_Objects.md#URLObject)             | The URL of the video or audio to play. An empty string (`""`) indicates that this information is unavailable for this card.    |
| `subType`                   | string  | The type of this card. Available types are: <ul><li><code>Type1</code></li><li><code>Type2</code></li><li><code>Type3</code></li><li><code>Type4</code></li></ul><div class="note"><p><strong>Note!</strong></p><p><code>Type1</code>, <code>Type2</code>, <code>Type3</code>, <code>Type5</code>, <code>Type6</code> are displayed as an <strong>empty string</strong>. You must determine the type by checking the fields of the <code>card</code> object.</p></div>  |
| `type`                      | string  | The type of this template. The value is always `"CardList"`.                                                                       |

## Template example

{% raw %}
```json
// Example for Type1 and Type2
// User requests to get a recommendation on some horror movies
{
  "subType": "",
  "type": "CardList",
  "cardList": [
    {
      "description": [
        {
          "type": "string",
          "value": "horror, thriller"
        },
        {
          "type": "string",
          "value": "Brown, Sally, Boss, Edward, Leonard, Pangyo, Choco"
        },
        {
          "type": "string",
          "value": ""
        }
      ],
      "imageUrl": {
        "type": "url",
        "value": "http://movie.phinf.naver.net/20170410_12/1491786049305s4W0n_JPEG/movie_image.jpg?type=w640_2"
      },
      "linkUrl": {
        "type": "url",
        "value": "http://movie.naver.com/movie/bi/mi/basic.nhn?code=118965"
      },
      "press": {
        "type": "string",
        "value": ""
      },
      "publishDate": {
        "type": "date",
        "value": ""
      },
      "referenceText": {
        "type": "string",
        "value": "NAVER search result"
      },
      "referenceUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=+%ec%98%81%ed%99%94"
      },
      "title": {
        "type": "string",
        "value": "Time to go home"
      },
      "videoUrl": {
        "type": "url",
        "value": ""
      }
    },
    {
      "description": [
        {
          "type": "string",
          "value": "horror"
        },
        {
          "type": "string",
          "value": "Cony, Jessica, Choco, Sally"
        },
        {
          "type": "string",
          "value": ""
        }
      ],
      "imageUrl": {
        "type": "url",
        "value": "http://movie.phinf.naver.net/20170317_53/1489741954272MquSW_JPEG/movie_image.jpg?type=w640_2"
      },
      "linkUrl": {
        "type": "url",
        "value": "http://movie.naver.com/movie/bi/mi/basic.nhn?code=137909"
      },
      "press": {
        "type": "string",
        "value": ""
      },
      "publishDate": {
        "type": "date",
        "value": ""
      },
      "referenceText": {
        "type": "string",
        "value": "NAVER search result"
      },
      "referenceUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=+%ec%98%81%ed%99%94"
      },
      "title": {
        "type": "string",
        "value": "Pokopang Rulz"
      },
      "videoUrl": {
        "type": "url",
        "value": ""
      }
    },
    ...
  ]
}

// Example for Type3
// User requests to play some video clips on game plays
{
  "subType": "",
  "type": "CardList",
  "cardList": [
    {
      "description": [
        {
          "type": "string",
          "value": "04:14"
        },
        {
          "type": "string",
          "value": ""
        },
        {
          "type": "string",
          "value": ""
        }
      ],
      "imageUrl": {
        "type": "url",
        "value": "http://hol.phinf.naver.net/00/587/820/58782072_0.jpg"
      },
      "linkUrl": {
        "type": "url",
        "value": ""
      },
      "press": {
        "type": "string",
        "value": ""
      },
      "publishDate": {
        "type": "date",
        "value": ""
      },
      "referenceText": {
        "type": "string",
        "value": "NAVER search result"
      },
      "referenceUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%ec%b6%95%ea%b5%ac+%eb%8f%99%ec%98%81%ec%83%81+%eb%b3%b4%ec%97%ac%ec%a4%98"
      },
      "title": {
        "type": "string",
        "value": "LINE Rangers - [Mega update] New Ultimate Evolved Rangers Ready for Battle!
"
      },
      "videoUrl": {
        "type": "url",
        "value": "http://m.tv.naver.com/v/1720910"
      }
    },
    {
      "description": [
        {
          "type": "string",
          "value": "06:31"
        },
        {
          "type": "string",
          "value": ""
        },
        {
          "type": "string",
          "value": ""
        }
      ],
      "imageUrl": {
        "type": "url",
        "value": "http://hol.phinf.naver.net/00/587/815/58781581_0.jpg"
      },
      "linkUrl": {
        "type": "url",
        "value": ""
      },
      "press": {
        "type": "string",
        "value": ""
      },
      "publishDate": {
        "type": "date",
        "value": ""
      },
      "referenceText": {
        "type": "string",
        "value": "NAVER search result"
      },
      "referenceUrl": {
        "type": "url",
        "value": "https://m.search.naver.com/search.naver?where=m&sm=mob_lic&query=%ec%b6%95%ea%b5%ac+%eb%8f%99%ec%98%81%ec%83%81+%eb%b3%b4%ec%97%ac%ec%a4%98"
      },
      "title": {
        "type": "string",
        "value": "LINE Rangers - EP04. Defeat Nut and his friends!"
      },
      "videoUrl": {
        "type": "url",
        "value": "http://m.sports.naver.com/video.nhn?id=310230"
      }
    },
    ...
  ]
}

// Example for Type4
// User requests for the latest news
{
  "subType": "Type4",
  "type": "CardList",
  "cardList": [
    {
      "description": [
        {
          "type": "string",
          "value": "Moon says Nooooooooooooooo to Boss's rival"
        },
        {
          "type": "string",
          "value": ""
        },
        {
          "type": "string",
          "value": ""
        }
      ],
      "imageUrl": {
        "type": "url",
        "value": ""
      },
      "linkUrl": {
        "type": "url",
        "value": "http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=105&oid=001&aid=0009767560"
      },
      "press": {
        "type": "string",
        "value": "LINE Today"
      },
      "publishDate": {
        "type": "date",
        "value": "2017-05-28"
      },
      "referenceText": {
        "type": "string",
        "value": ""
      },
      "referenceUrl": {
        "type": "url",
        "value": ""
      },
      "title": {
        "type": "string",
        "value": "Moon says No! to Boss"
      },
      "videoUrl": {
        "type": "url",
        "value": ""
      }
    },
    {
      "description": [
        {
          "type": "string",
          "value": "TOKYO – December 27, 2017 – To mark the second anniversary of the launch of its live streaming service LINE LIVE, LINE Corporation has released LINE LIVE 2017: By the Numbers — a report that summarizes how viewers and broadcasters use the service..."
        },
        {
          "type": "string",
          "value": ""
        },
        {
          "type": "string",
          "value": ""
        }
      ],
      "imageUrl": {
        "type": "url",
        "value": ""
      },
      "linkUrl": {
        "type": "url",
        "value": "http://news.naver.com/main/read.nhn?mode=LSD&mid=sec&sid1=001&oid=001&aid=0009297247"
      },
      "press": {
        "type": "string",
        "value": "LINE Press"
      },
      "publishDate": {
        "type": "date",
        "value": "2017-12-27"
      },
      "referenceText": {
        "type": "string",
        "value": ""
      },
      "referenceUrl": {
        "type": "url",
        "value": ""
      },
      "title": {
        "type": "string",
        "value": "[Japan] LINE LIVE 2017: By the Numbers"
      },
      "videoUrl": {
        "type": "url",
        "value": ""
      }
    },
    ...
  ]
}

```
{% endraw %}

## UI example {#UIExample}

The following examples show how each card type is used to present information on the Clova app distributed by {{ book.OrientedService }}.

| `Type1` | `Type2` |
|:-------:|:-------:|
| ![Type1](/CIC/Resources/Images/Content_Template-Content_Card_Type.png) | ![Type2](/CIC/Resources/Images/Content_Template-Content_Card_with_Link_Type.png) |

| `Type3` | `Type4` |
|:-------:|:-------:|
| ![Type3](/CIC/Resources/Images/Content_Template-Video_Card_Type.png) | ![Type4](/CIC/Resources/Images/Content_Template-News_Card_Type.png) |

<div class="note">
<p><strong>Note!</strong></p>
<p>UI examples for <code>Type5</code> and <code>Type6</code> are in preparation.</p>
</div>

## See also

* [ImageList](/CIC/References/ContentTemplates/ImageList.md)
* [ImageText](/CIC/References/ContentTemplates/ImageText.md)
* [Popup](/CIC/References/ContentTemplates/Popup.md)
* [Text](/CIC/References/ContentTemplates/Text.md)
