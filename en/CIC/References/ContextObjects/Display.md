## Device.Display {#Display}

`Device.Display` is a format for reporting to CIC the display information of the client device. By providing the display information to Clova, the client will be supplied with visual content in the best resolution and DPI for the client. If client does not provide its display information to Clova, Clova assumes the client has a full HD resolution.

### Object structure

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "Display"
  },
  "payload": {
    "contentLayer": {
      "width": {{number}},
      "height": {{number}}
    },
    "dpi": {{number}},
    "orientation": {{string}},
    "size": {{string}}
  }
}
```

{% endraw %}

### Payload fields

| Field       | Type    | Description                     | Required |
|---------------|:---------:|-----------------------------|:---------:|
| `contentLayer`        | object | Contains the resolution of the client display for contents. This field is mandatory if the `size` field is `"custom"`.  | Optional |
| `contentLayer.width`  | number | The width of the display in pixels.        | Required |
| `contentLayer.height` | number | The height of the display in pixels.       | Required |
| `dpi`         | number | The DPI of the display. This field is omissible _only if_ the `size` field is `"none"`.     | Optional |
| `orientation` | string | The orientation of the physical screen of the client: <ul><li><code>"landscape"</code></li><li><code>"portrait"</code></li></ul>This field is omissible _only if_ the `size` field is `"none"`.  | Optional |
| `size`        | string | The resolution of the display. Available values are: <ul><li><code>"none"</code>: The client has no display</li><li><code>"s100"</code>: Low resolution (160x107 pixels)</li><li><code>"m100"</code>: Medium resolution (427x240 pixels)</li><li><code>"l100"</code>: High resolution (640x360 pixels)</li><li><code>"xl100"</code>: Ultra high resolution (xlarge type, 899x506 pixels)</li><li><code>"custom"</code>: For unavailable resolution, assign `"custom"` here and define the actual resolution in the `contentLayer` field. </li></ul>  | Required |

### Example

{% raw %}

```json
{
  "header": {
    "namespace": "Device",
    "name": "Display"
  },
  "payload": {
    "orientation": "portrait",
    "dpi": 320,
    "size": "custom",
    "customLayer": {
      "width": 640,
      "heigjt": 280,
    }
  }
}
```

{% endraw %}

### See also

* [`SpeechRecognizer.Recognize`](/CIC/References/CICInterface/SpeechRecognizer.md#Recognize)
* [Custom extension message](/CEK/References/CEK_API.md#CustomExtMessage)
