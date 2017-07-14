# Clova Home extension message
A Clova Home extension message is used when your extension sends and receives messages to and from CEK to control IoT devices. A Clova Home extension message, whether it is a request or response, consists of *header* field and *payload* field. Configuration of the *payload* field can differ depending on which [Clova Home API](/CEK/References/Clova_Home_API.md) is used. The following explains the common format of a Clova Home extension message.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova Home extension message is divided to a request message and response message according to the API. A request message is sent from CEK to your extension using API with the name format, XxxxRequest. A response message is returned from your extension to CEK; its name format is either XxxxConfirmation or XxxxResponse. Also, return 200 OK HTTPS response even when an error occurs using API with the name format, XxxxError.</p>
</div>

## Message format
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
}
```
{% endraw %}


## Message field
| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| header                 | object | Header of the Clova Home extension message                                          | Yes     |
| header.messageId       | string | Message ID. It is created by Clova to identify individual messages (UUID).               | Yes     |
| header.name            | string | API name of the Clova Home extension message                                      | Yes     |
| header.namespace       | string | This field is fixed to "ClovaHome".                                          | Yes     |
| header.payloadVersion  | string | Clova Home API version specified in *header.name*. Configuration of the *payload* field can differ depending on the version.                                   | Yes     |
| payload                | object | Configuration and field values of the payload object can differ depending on which [Clova Home API](/CEK/References/Clova_Home_API.md) is specified in *header.name*. | Yes     |

## Message example
{% raw %}
```json
Example 1: DiscoverAppliancesRequest API - request message
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

Example 2: DiscoverAppliancesResponse API - response message
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

Example 3: IncrementTargetTemperatureConfirmation API - response message
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

Example 4: TargetOffLineError API - Error response message
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

## See also
* [Building Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md)
* [Clova Home API](/CEK/References/Clova_Home_API.md)