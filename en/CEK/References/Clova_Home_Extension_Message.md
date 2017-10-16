## Clova Home extension message {#ClovaHomeExtMessage}
A Clova Home extension message is a message specification used by your extension when it exchanges information with CEK to control IoT appliances. The following explains [message formats](#ClovaHomeExtMessageFormat) and [interfaces](#ClovaHomeExtInterface) of a Clova Home extension message.

### Message format {#ClovaHomeExtMessageFormat}

A Clova Home extension message consists of `header` and `payload` fields. This is same for both request and response messages. The `payload` field can have different configuration depending on which [interface](#ClovaHomeExtInterface) is used. The following explains the common format of a Clova Home extension message.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>A Clova Home extension message is divided into a request message and a response message. Request messages which are sent from CEK to an extension have a name format of `XxxxRequest`. Response messages which are sent from an extension to CEK have a name format of `XxxxConfirmation` or `XxxxResponse`. Also, even when an error occurs, you must return a 200 OK HTTPS response. Such response messages have a name format of `XxxxError`.</p>
</div>

#### Message structure

{% raw %}

```json
{
  "header": {
    "messageId": {{string}},
    "namespace": {{string}},
    "name": {{string}},
    "payloadVersion": {{string}}
  },
  "payload": {{object}}
}
```

{% endraw %}


#### Message field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `header`                 | object | The header of the message                                                                 | Yes     |
| `header.messageId`       | string | The message ID. An identifier (UUID) created by Clova to distinguish individual messages.              | Yes     |
| `header.name`            | string | The API name of the message                                                             | Yes     |
| `header.namespace`       | string | The value is always `"ClovaHome"`.                                          | Yes     |
| `header.payloadVersion`  | string | The version of the Clova Home extension message specified in `header.name`. Configuration of the `payload` field can vary depending on the version.                                   | Yes     |
| `payload`                | object | Configuration of the payload object and its field values can vary depending on which [interface](#ClovaHomeExtInterface) is specified in `header.name`. | Yes     |

#### Message example

{% raw %}

```json
Example 1: DiscoverAppliancesRequest - request message
{
  "header": {
    "messageId": "8ddd7f05-7703-4cb4-a6dd-93c209c6647b",
    "name": "DiscoverAppliancesRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33"
  }
}

Example 2: DiscoverAppliancesResponse - response message
{
  "header": {
    "messageId": "99f9d8ff-9366-4cab-a90c-b4c7eca0abbe",
    "name": "DiscoverAppliancesResponse",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "discoveredAppliances": [
      {
        "applianceId": "device-001",
        "manufacturerName": "device-manufacturer-name",
        "modelName": "스마트 전등",
        "version": "v1.0",
        "friendlyName": "거실 전등",
        "friendlyDescription": "스마트폰으로 제어할 수 있는 전등",
        "isReachable": true,
          "actions": [
            "TurnOn",
            "TurnOff"
        ],
        "applianceTypes": ["LIGHT"],
        "additionalApplianceDetails": {
        }
      },
      {
        "applianceId": "device-002",
        "manufacturerName": "device-manufacturer-name",
        "modelName": "스마트 플러그",
        "version": "v1.0",
        "friendlyName": "부엌 플러그",
        "friendlyDescription": "에너지를 절약하는 플러그",
        "isReachable": true,
        "actions": [
          "TurnOn",
          "TurnOff"
        ],
        "applianceTypes": ["SMARTPLUG"],
        "additionalApplianceDetails": {
        }
      }
    ]
  }
}

Example 3: IncrementTargetTemperatureConfirmation - response message
{
  "header": {
    "messageId": "4ec35000-88ce-4724-b7e4-7f52050558fd",
    "name": "IncrementTargetTemperatureConfirmation",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "targetTemperature": {
      "value": 25.0
    },
    "previousState": {
      "targetTemperature": {
        "value": 22.0
      }
    }
  }
}

Example 4: TargetOffLineError - Error response message
{
  "header": {
    "messageId": "fef949b7-eb94-4bda-a417-2cfb604194c3",
    "namespace": "ClovaHome",
    "name": "TargetOfflineError",
    "payloadVersion": "1.0"
  },
  "payload": {
  }
}
```

{% endraw %}

#### See also
* [Building Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md)
* [Interface](#ClovaHomeExtInterface)

### Interface {#ClovaHomeExtInterface}
Clova Home extension messages are categorized into the following interfaces.

* Interface
  * [Discovery interface](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md)
  * [Control interface](/CEK/References/ClovaHomeInterface/Control_Interfaces.md)
  * [Error interface](/CEK/References/ClovaHomeInterface/Error_Interfaces.md)

* Shared objects
  * [Shared objects](#SharedObjects)
