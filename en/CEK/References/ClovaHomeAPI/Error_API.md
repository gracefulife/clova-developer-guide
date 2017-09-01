## Error API {#ErrorAPI}
Use this API to have your Clova Home extension return errors to CEK.


| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`DriverInternalError`](#DriverInternalError) | Error Response | Return this response message to CEK when an internal error occurs.             |
| [`TargetOfflineError`](#TargetOfflineError)   | Error Response | Return this response message to CEK when the target appliance is not accessible (offline). |
| [`ValueOutOfRangeError`](#ValueOutOfRangeError) | Error Resposne | Return this response message to CEK when a user requests an action which is out of range on the target appliance. |

<div class="note">
<p><strong>Note!</strong></p>
<p>Other types of error messages will be added going forward.</p>
</div>

### DriverInternalError {#DriverInternalError}
Return this response message to CEK when an internal error occurs. When CEK receives this message, it forwards a pre-defined error message to the client.

#### Payload field

None

#### Remarks
* Return a 200 OK HTTP response to CEK even when it is an error message.
* Error messages do not require a body (payload) because their names clearly express situations.

#### Message example

{% raw %}
```json
{
  "header": {
    "messageId": "fef949b7-eb94-4bda-a417-2cfb604194c3",
    "namespace": "ClovaHome",
    "name": "DriverInternalError",
    "payloadVersion": "1.0"
  },
  "payload": {
  }
}
```
{% endraw %}

#### See also
* [`TargetOfflineError`](#TargetOfflineError)

### TargetOfflineError {#TargetOfflineError}
Return this response message to CEK when the target appliance is not accessible (offline). When CEK receives this message, it forwards a pre-defined error message to the client.

#### Payload field

None

#### Remarks
* Return a 200 OK HTTP response to CEK even when it is an error message.
* Error messages do not require a body (payload) because their names clearly express situations.

#### Message example

{% raw %}
```json
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
* [`DriverInternalError`](#DriverInternalError)

### ValueOutOfRangeError {#ValueOutOfRangeError}
Return this response message to CEK when a user requests an action which is out of range on the target appliance. For example, if an air conditioner allows a temperature range of 18 to 28 and a user requests to set it to 16 or 30, you can return this message. The `payload` field must have the maximum and minimum values allowed on the target appliance.

#### Payload field

| Field name       | Type    | Field description                     | Required |
|---------------|---------|-----------------------------|---------|
| `maximumValue` | number | The maximum value allowed on the target appliance | Yes    |
| `minimumValue` | number | The minimum value allowed on the target appliance | Yes    |

#### Remarks
You can use values of `payload` to guide users.

#### Message example

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

#### See also
* [`DriverInternalError`](#DriverInternalError)