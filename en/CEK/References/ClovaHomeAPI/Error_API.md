## Error API {#ErrorAPI}
Use this API to have your Clova Home extension return errors to CEK.


| Message name  | Message type  | Message description  |
|------------------|-----------|---------------------------------------------|
| [`DriverInternalError`](#DriverInternalError)  | Error response | Return this response message to CEK when an internal error has occurred.  |
| [`TargetOfflineError`](#TargetOfflineError)  | Error response | Return this response message to CEK when the target appliance is not accessible (offline). |

### DriverInternalError {#DriverInternalError}
Return this response message to CEK when an internal error has occurred. When CEK receives this message, it forwards a pre-defined error message to the client.

#### Payload field

None

#### Remarks
* Return 200 OK HTTP response to CEK even when it is an error message.
* Error messages do not need a body (payload) because their names clearly express situations.

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

### TargetOfflineError{#TargetOfflineError}
Return this error response to CEK when the target appliance is not accessible (offline). When CEK receives this message, it forwards a pre-defined error message to the client.

#### Payload field

None

#### Remarks
* Return 200 OK HTTP response to CEK even when it is an error message.
* Error messages do not need a body (payload) because their names clearly express situations.

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