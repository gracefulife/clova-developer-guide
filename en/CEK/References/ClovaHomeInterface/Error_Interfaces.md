# Error
The error interfaces are used when the Clova Home extension returns errors to CEK.


| Message name         | Type  | Description                                   |
|------------------|-----------|---------------------------------------------|
| [`ConditionsNotMetError`](#ConditionsNotMetError)          | Error response | Sent to CEK as a response if a certain condition (state) required for operating the target appliance is not satisfied. |
| [`DeviceFailureError`](#DeviceFailureError)                | Error response | Sent to CEK as a response if a defect occurs in the target appliance.              |
| [`DriverInternalError`](#DriverInternalError)              | Error response | Sent to CEK as a response if an internal error occurs.                |
| [`ExpiredAccessTokenError`](#ExpiredAccessTokenError)      | Error response | Sent to CEK as a response if the access token received from the [authorization server](/CEK/Guides/Link_User_Account.md#BuildAuthServer) at [account linking](/CEK/Guides/Link_User_Account.md) is expired.  |
| [`InvalidAccessTokenError`](#InvalidAccessTokenError)      | Error response | Sent to CEK as a response if the user has disabled the permission on the access token being used.         |
| [`NoSuchTargetError`](#NoSuchTargetError)                  | Error response | Sent to CEK as a response if the target device is not found.                            |
| [`NotSupportedInCurrentModeError`](#NotSupportedInCurrentModeError) | Error response | Sent to CEK as a response if the directed action cannot be performed under the current mode of the target device.  |
| [`TargetOfflineError`](#TargetOfflineError)                | Error response | Sent to CEK as a response if the target device is offline and cannot be connected. |
| [`UnsupportedOperationError`](#UnsupportedOperationError)  | Error response | Sent to CEK as a response if an unsupported action of the target appliance is requested.   |
| [`ValueOutOfRangeError`](#ValueOutOfRangeError)            | Error response | Sent to CEK as a response if the action request is outside of the range that can be processed by the target device. |

<div class="note">
<p><strong>Note!</strong></p>
<p>More error message types will be added soon.</p>
</div>

## ConditionsNotMetError {#ConditionsNotMetError}
Sent to CEK as a response if a certain condition (state) required for operating the target appliance is not satisfied. When CEK receives this message, a predefined error message is sent to the client.

### Payload fields

None

### Remarks
* The extension must send the error messages to CEK as a normal HTTPS response (200 OK).
* A separate payload is not required because the names of the error messages provide information on the situation.

### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "4ea1e527-7be3-4b54-b531-93d245b97303",
    "namespace": "ClovaHome",
    "name": "ConditionsNotMetError",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```
{% endraw %}

### See also
* [`NotSupportedInCurrentModeError`](#NotSupportedInCurrentModeError)

## DeviceFailureError {#DeviceFailureError}
Sent to CEK as a response if a defect occurs in the target appliance. When CEK receives this message, a predefined error message is sent to the client.

### Payload fields

None

### Remarks
* The extension must send the error messages to CEK as a normal HTTPS response (200 OK).
* A separate payload is not required because the names of the error messages provide information on the situation.

### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "4ea1e527-7be3-4b54-b531-93d245b97303",
    "namespace": "ClovaHome",
    "name": "DeviceFailureError",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```
{% endraw %}

### See also
* [`DriverInternalError`](#DriverInternalError)
* [`TargetOfflineError`](#TargetOfflineError)

## DriverInternalError {#DriverInternalError}
Sent to CEK as a response if an internal error occurs. When CEK receives this message, a predefined error message is sent to the client.

### Payload fields

None

### Remarks
* The extension must send the error messages to CEK as a normal HTTPS response (200 OK).
* A separate payload is not required because the names of the error messages provide information on the situation.

### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "fef949b7-eb94-4bda-a417-2cfb604194c3",
    "namespace": "ClovaHome",
    "name": "DriverInternalError",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```
{% endraw %}

### See also
* [`DeviceFailureError`](#DeviceFailureError)
* [`TargetOfflineError`](#TargetOfflineError)

## ExpiredAccessTokenError {#ExpiredAccessTokenError}
Sent to CEK as a response if the access token received from the [authorization server](/CEK/Guides/Link_User_Account.md#BuildAuthServer) at [account linking](/CEK/Guides/Link_User_Account.md) is expired. When CEK receives this message, a predefined error message is sent to the client.

### Payload fields

None

### Remarks
* The extension must send the error messages to CEK as a normal HTTPS response (200 OK).
* A separate payload is not required because the names of the error messages provide information on the situation.

### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "1abd6113-4a36-47c3-851e-bee3254fe183",
    "namespace": "ClovaHome",
    "name": "ExpiredAccessTokenError",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```
{% endraw %}

### See also
* [`InvalidAccessTokenError`](#InvalidAccessTokenError)

## InvalidAccessTokenError {#InvalidAccessTokenError}
Sent to CEK as a response if the user has disabled the permission on the access token being used. When CEK receives this message, a predefined error message is sent to the client.

### Payload fields

None

### Remarks
* The extension must send the error messages to CEK as a normal HTTPS response (200 OK).
* A separate payload is not required because the names of the error messages provide information on the situation.

### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "b8ac8b45-9fb9-4dc4-97ca-d55e9fc1ff8f",
    "namespace": "ClovaHome",
    "name": "InvalidAccessTokenError",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```
{% endraw %}

### See also
* [`ExpiredAccessTokenError`](#ExpiredAccessTokenError)

## NoSuchTargetError {#NoSuchTargetError}
Sent to CEK as a response if the target device is not found. For example, this message must be sent if the user has deleted an appliance from an IoT service, but a control request for the appliance has been made before the information is reflected on the Clova app. When CEK receives this message, a predefined error message is sent to the client.

### Payload fields

None

### Remarks
* The extension must send the error messages to CEK as a normal HTTPS response (200 OK).
* A separate payload is not required because the names of the error messages provide information on the situation.

### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "d458e46c-6827-4940-9340-a7a9d427d7ab",
    "namespace": "ClovaHome",
    "name": "NoSuchTargetError",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```
{% endraw %}

### See also
* [`ConditionsNotMetError`](#ConditionsNotMetError)
* [`TargetOfflineError`](#TargetOfflineError)

## NotSupportedInCurrentModeError {#NotSupportedInCurrentModeError}
Sent to CEK as a response if the directed action cannot be performed under the current mode of the target device. For example, template-related controls may be restricted for some air conditioners operating in dehumidifier mode. This message must be sent to users of those products if a control request for temperature is made in dehumidifier mode. When CEK receives this message, a predefined error message is sent to the client.

### Payload fields

None

### Remarks
* The extension must send the error messages to CEK as a normal HTTPS response (200 OK).
* A separate payload is not required because the names of the error messages provide information on the situation.

### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "f321b946-b593-4279-a840-8e5af5a00146",
    "namespace": "ClovaHome",
    "name": "NotSupportedInCurrentModeError",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```
{% endraw %}

### See also
* [`UnsupportedOperationError`](#UnsupportedOperationError)
* [`ValueOutOfRangeError`](#ValueOutOfRangeError)

## TargetOfflineError {#TargetOfflineError}
Sent to CEK as a response if the target device is offline and cannot be connected. When CEK receives this message, a predefined error message is sent to the client.

### Payload fields

None

### Remarks
* The extension must send the error messages to CEK as a normal HTTPS response (200 OK).
* A separate payload is not required because the names of the error messages provide information on the situation.

### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "fef949b7-eb94-4bda-a417-2cfb604194c3",
    "namespace": "ClovaHome",
    "name": "TargetOfflineError",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```
{% endraw %}

### See also
* [`DeviceFailureError`](#DeviceFailureError)
* [`DriverInternalError`](#DriverInternalError)

## UnsupportedOperationError {#UnsupportedOperationError}

Sent to CEK as a response if an unsupported action of the target appliance is requested. If the user requests an action that is unsupported by default, CEK informs the user immediately that the request is not within the permitted range. However, the permitted range of actions such as `SetMode` cannot be checked until the Clova Home extension receives the [SetModeRequest](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetModeRequest) message and checks the `mode` field value. When the Clova Home extension sends a message and the action is not supported, an error response must be sent. The `UnsupportedOperationError` message can be used to send to CEK.

For example, let us assume that the user’s thermostat (`"THERMOSTAT"` type) can perform the `SetMode` action and it supports `"sleep"` and `"away"` modes. If the user requests to set the `"cool"` mode on the appliance, the Clova Home extension must send an `UnsupportedOperationError` message to CEK.

### Payload fields

None

### Remarks
* The extension must send the error messages to CEK as a normal HTTPS response (200 OK).
* A separate payload is not required because the names of the error messages provide information on the situation.

### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "e9a77ef6-748b-4f9b-aa3e-c14ece3fa726",
    "namespace": "ClovaHome",
    "name": "UnsupportedOperationError",
    "payloadVersion": "1.0"
  },
  "payload": {}
}
```
{% endraw %}

### See also
* [`NotSupportedInCurrentModeError`](#NotSupportedInCurrentModeError)
* [`ValueOutOfRangeError`](#ValueOutOfRangeError)

## ValueOutOfRangeError {#ValueOutOfRangeError}
Sent to CEK as a response if the action request is outside of the range that can be processed by the target device. For example, this message can be sent if a user requests to set a temperature such as 16 or 30 on the air conditioning when the available setting is 18-28. The `payload` field must send the maximum and minimum values that can be processed by the target appliance.

### Payload fields

| Field name       | Data type    | Description                     | Required |
|---------------|---------|-----------------------------|:---------:|
| `maximumValue` | number | Maximum setting value permitted on the target appliance. | Required    |
| `minimumValue` | number | Minimum setting value permitted on the target appliance. | Required    |

### Remarks
* The extension must send the error messages to CEK as a normal HTTPS response (200 OK).
* A separate payload is not required because the names of the error messages provide information on the situation.
* The values entered in `payload` fields can be used to inform users.

### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "fef949b7-eb94-4bda-a417-2cfb604194c3",
    "namespace": "ClovaHome",
    "name": "ValueOutOfRangeError",
    "payloadVersion": "1.0"
  },
  "payload": {
    "minimumValue":18.0,
    "maximumValue":30.0
  }
}
```
{% endraw %}

### See also
* [`UnsupportedOperationError`](#UnsupportedOperationError)
* [`NotSupportedInCurrentModeError`](#NotSupportedInCurrentModeError)
