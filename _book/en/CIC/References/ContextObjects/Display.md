## Device.Display {#Display}
`Device.Display` is a message format applied to report the display information of the device of the client to CIC. When sending display information owned by the client device to Clova, a media content with a resolution corresponding to the screen ratio and DPI will be returned.  If the context information is not sent to CIC, Clova will assume that the client owns a display with Full HD resolution.  A content with resolution corresponding to the client device or the same ratio as the resolution will be provided if using the context information. 

### Message structure
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

### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `contentLayer`        | object | An object containing resolution information of a display part displaying content. This field cannot be omitted if the value of `size` is `"custom"`.  | No |
| `contentLayer.width`  | number | The width of content being displayed on the display. Its unit is pixel(px).                                           | Yes |
| `contentLayer.height` | number | The height of content being displayed on the display. Its unit is pixel(px).                                           | Yes |
| `dpi`         | number | DPI of the display device. This field can be omitted if the value of `size` is `"none"`.                                 | No |
| `orientation` | string | Direction of the display device. This field can be omitted if the value of `size` is `"none"`.<ul><li><code>"landscape"</code>: Horizontal direction</li><li><code>"portrait"</code>: Vertical direction</li></ul>  | No |
| `size`        | string | A value that indicates volume of the resolution of the display device. A value indicating the resolution size of the display device. In the value, a pre-defined number or a value implying any resolution size or a value meaning no display can be entered. Available values are: <ul><li><code>"none"</code>: No display found from the client appliance</li><li><code>"s100"</code>: Low resolution (160px X 107px)</li><li><code>"m100"</code>: Medium resolution (427px X 240px)</li><li><code>"l100"</code>: High resolution (640px X 360px)</li><li><code>"xl100"</code>: Ultra high resolution (xlarge type, 899px X 506px)</li><li><code>"custom"</code>: A resolution without a set standard Enter the actual resolution value of the device on the `contentLayer` field. </li></ul> | Yes |


### Message example
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