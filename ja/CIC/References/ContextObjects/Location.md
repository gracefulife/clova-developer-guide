## Clova.Location {#Location}
`Clova.Location`は、クライアントの現在位置情報をCICにレポートするときに使用されるメッセージ形式です。GPS、基地局、ネットワークデバイスなどによって把握された位置情報をCICに送信します。

### Object structure
{% raw %}
```json
{
  "header": {
    "namespace": "Clova",
    "name": "Location"
  },
  "payload": {
    "latitude": {{string}},
    "longitude": {{string}},
    "refreshedAt": {{string}}
  }
}
```
{% endraw %}

### Payload fields

| フィールド名       | データ型    | 説明                     | 必須/任意 |
|---------------|---------|-----------------------------|:---------:|
| `latitude`      | string  | 緯度                                                                                     | 必須 |
| `longitude`     | string  | 経度                                                                                     | 必須 |
| `refreshedAt`   | string  | 位置の最終確認時刻(UTC基準、<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>形式) | 必須 |

### Object example
{% raw %}
```json
{
  "header": {
    "namespace": "Clova",
    "name": "Location"
  },
  "payload": {
    "latitude": "37.3594915",
    "longitude": "127.1032242",
    "refreshedAt": "2017-04-06T13:34:15.074361+08:28"
  }
}
```
{% endraw %}

### 次の項目も参照してください。
* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
