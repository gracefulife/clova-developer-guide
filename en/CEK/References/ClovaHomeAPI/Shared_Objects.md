## Shared objects {#SharedObjects}
Include the following shared objects in a message body (payload) when you send an event message using the Clova Home API.

| Object name                             | Object description                       |
| --------------------------------------- | ---------------------------------------- |
| [ApplianceObject](#ApplianceObject)     | Object containing information of the IoT appliance |
| [TemperatureObject](#TemperatureObject) | Object containing temperature information |

### ApplianceObject {#ApplianceObject}
This is an object containing information of the IoT appliance. Use this object to return CEK of the list of appliances registered to a user account or to request Clova Home extension to control an appliance.

#### Object field
| Field name                 | Type         | Field description                        | Required |
| -------------------------- | ------------ | ---------------------------------------- | -------- |
| actions[]                  | string array | List of actions supported on the appliance. A user can request to perform control actions which are supported on the appliance. | No       |
| additionalApplianceDetails | object       | Field reserved to receive additional information from a manufacturer or IoT service | No       |
| applianceId                | string       | Appliance ID                             | Yes      |
| applianceTypes[]           | string array | Appliance type. Available values are:<ul><li>LIGHT: Lighting appliance type</li><li>SMARTLOCK: Door lock type</li><li>SWITCH: Switch for controlling power socket</li><li>SMARTPLUG: Plug for controlling appliance power</li></ul> | Yes      |
| friendlyName               | string       | Appliance name specified by the user     | No       |
| friendlyDescription        | string       | Description of the appliance             | No       |
| isReachable                | boolean      | Whether it is controllable remotely <ul><li>true: Controllable remotely</li><li>false: Not controllable remotely</li></ul> | No       |
| manufacturerName           | string       | Manufacturer name of the appliance       | No       |
| modelName                  | string       | Model name of the appliance              | No       |
| version                    | string       | Software version of the manufacturer     | No       |

### Remarks
When you request a list of user appliances using the *[DiscoverAppliancesRequest](#DiscoverAppliancesRequest)* message, your Clova Home extension must fill in every field except for *additionalApplianceDetails*.

#### Object Example
{% raw %}
```json
// Example 1: DiscoverAppliancesResponse message
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

// Example 2: TurnOnRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "TurnOnRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-001"
    }
  }
}
```
{% endraw %}

#### See also
* [ClovaHome.DiscoverAppliancesResponse](DiscoverAppliancesResponse)
* [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest)
* [DiscoverAppliancesRequest](#DiscoverAppliancesRequest)
* [GetLockStateRequest](#GetLockStateRequest)
* [GetTargetTemperatureRequest](#GetTargetTemperatureRequest)
* [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest)
* [SetLockStateRequest](#SetLockStateRequest)
* [TurnOffRequest](#TurnOffRequest)
* [TurnOnRequest](#TurnOnRequest)

### TemperatureObject {#TemperatureObject}
This is an object containing temperature information. It displays expected change in temperature or target temperature before and after changing it. The value is displayed to one decimal point.

#### Object field
| Field name | Type   | Field description  | Required |
| ---------- | ------ | ------------------ | -------- |
| value      | number | Temperature value. | Yes      |

#### Object Example
{% raw %}
```json
// Example 1: IncrementTargetTemperatureRequest message
{
  "header": {
    "messageId": "6c04fc2d-64dd-41a0-9162-7cb0d4cf7c08",
    "name": "IncrementTargetTemperatureRequest",
    "namespace": "ClovaHome",
    "payloadVersion": "1.0"
  },
  "payload": {
    "accessToken": "92ebcb67fe33",
    "appliance": {
      "applianceId": "device-001"
    },
    "deltaTemperature": {
      "value": 1.0
    }
  }
}

// Example 2: IncrementTargetTemperatureConfirmation message
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
        "value": 21.0
      }
    }
  }
}
```
{% endraw %}

#### See also
* [DecrementTargetTemperatureRequest](#DecrementTargetTemperatureRequest)
* [DecrementTargetTemperatureConfirmation](#DecrementTargetTemperatureConfirmation)
* [GetTargetTemperatureRequest](#GetTargetTemperatureRequest)
* [GetTargetTemperatureResponse](#GetTargetTemperatureResponse)
* [IncrementTargetTemperatureRequest](#IncrementTargetTemperatureRequest)
* [IncrementTargetTemperatureConfirmation](#IncrementTargetTemperatureConfirmation)