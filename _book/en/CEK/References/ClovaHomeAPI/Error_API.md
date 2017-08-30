## Error API {#ErrorAPI}
Use this API to have your Clova Home extension return errors to CEK.


| Message name         | Message type  | Message description                                   |
|------------------|-----------|---------------------------------------------|
| [`DriverInternalError`](#DriverInternalError)                                 | Error Response | Return this response message to CEK when an internal error occurs.             |
| [`TargetOfflineError`](#TargetOfflineError)                                   | Error Response | Return this response response to CEK when the target appliance is not accessible (offline). |

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

### TargetOfflineError{#TargetOfflineError}
Return this error response to CEK when the target appliance is not accessible (offline). When CEK receives this message, it forwards a pre-defined error message to the client.

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