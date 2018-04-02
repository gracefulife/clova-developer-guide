## Clova Home extension messages {#ClovaHomeExtMessage}
Clova Home extension messages are exclusively used when an extension controlling IoT devices exchange information with CEK. This section explains the [message format](#ClovaHomeExtMessageFormat) and [interface](#ClovaHomeExtInterface) of Clova Home extension messages.

### Message format {#ClovaHomeExtMessageFormat}

Clova Home extension messages are configured with the `header` field and `payload` field. This is the same for both request messages and response messages. However, the configuration of the `payload` field may vary depending on the [interface](#ClovaHomeExtInterface) used. The following explains the common format of the Clova Home extension messages.

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova Home extension messages are classified into request and response messages. Request messages sent from CEK to an extension are in the `XxxxRequest` format and response messages sent from an extension to CEK are in the `XxxxConfirmation` or `XxxxResponse` format. In addition, a normal HTTPS response (200 OK) must be sent even when an error occurs, and this response message must have the same name as `XxxxError`.</p>
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


#### Message fields
| Field       | Data Type    | Description                     | Required/Included |
|---------------|---------|-----------------------------|:-------------:|
| `header`                 | object | The header of the message.                                                                                            | Required/Always     |
| `header.messageId`       | string | The message ID (UUID). This is an identifier created by Clova to distinguish individual messages.                                         | Required/Always     |
| `header.name`            | string | The API name of the message.                                                                                        | Required/Always     |
| `header.namespace`       | string | This field is always set to `"ClovaHome"`.                                                                     | Required/Always     |
| `header.payloadVersion`  | string | The version of the Clova Home extension message specified in `header.name`. Configuration of the `payload` field may vary depending on this version.  | Required/Always     |
| `payload`                | object | The configuration and field value of payload objects vary depending on the [interface](#ClovaHomeExtInterface) assigned to `header.name`.       | Required/Always     |

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
        "modelName": "Smart lamp",
        "version": "v1.0",
        "friendlyName": "Living room lamp",
        "friendlyDescription": "A lamp that can be controlled using a smartphone",
        "isReachable": true,
          "actions": [
            "DecrementBrightness",
            "HealthCheck",
            "IncrementBrightness",
            "SetBrightness",
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
        "modelName": "Smart plug",
        "version": "v1.0",
        "friendlyName": "Kitchen plug",
        "friendlyDescription": "An energy-saving plug",
        "isReachable": true,
        "actions": [
          "HealthCheck",
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

Example 4: TargetOffLineError - error response message
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
* [Creating a Clova Home extension](/CEK/Guides/Build_Clova_Home_Extension.md)
* [Interface](#ClovaHomeExtInterface)

### Interface {#ClovaHomeExtInterface}
The interfaces of Clova Home extension messages are classified as follows:

* Interface
  * [Discovery interface](/CEK/References/ClovaHomeInterface/Discovery_Interfaces.md)
  * [Control interface](/CEK/References/ClovaHomeInterface/Control_Interfaces.md)
  * [Error interface](/CEK/References/ClovaHomeInterface/Error_Interfaces.md)

* Shared objects
  * [Shared objects](/CEK/References/ClovaHomeInterface/Shared_Objects.md)
