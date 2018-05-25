# Error
Clova Home ExtensionがCEKにエラーを返す際に使用されるインターフェースです。


| メッセージ         | タイプ  | 説明                                   |
|------------------|-----------|---------------------------------------------|
| [`ConditionsNotMetError`](#ConditionsNotMetError)          | Error Response | エンドポイントが動作するための特定の条件(ステータス)が満たされていない場合、CEKにこのメッセージをレスポンスとして返します。 |
| [`DeviceFailureError`](#DeviceFailureError)                | Error Response | エンドポイントに障害が発生した場合、CEKにこのメッセージをレスポンスとして返します。              |
| [`DriverInternalError`](#DriverInternalError)              | Error Response | 内部エラーが発生した場合、CEKにこのメッセージをレスポンスとして返します。                |
| [`ExpiredAccessTokenError`](#ExpiredAccessTokenError)      | Error Response | [アカウントリンク](/CEK/Guides/Link_User_Account.md)の際、[認可サーバー](/CEK/Guides/Link_User_Account.md#BuildAuthServer)から発行されたアクセストークンが期限切れである場合、CEKにこのメッセージをレスポンスとして返します。  |
| [`InvalidAccessTokenError`](#InvalidAccessTokenError)      | Error Response | ユーザーが使用中のアクセストークンに対する権限を解除した場合、CEKにこのメッセージをレスポンスとして返します。         |
| [`NoSuchTargetError`](#NoSuchTargetError)                  | Error Response | エンドポイントが存在しない場合、このメッセージをレスポンスとして返します。                            |
| [`NotSupportedInCurrentModeError`](#NotSupportedInCurrentModeError) | Error Response | エンドポイントの現在のモードではサポートされないディレクティブを示します。  |
| [`TargetOfflineError`](#TargetOfflineError)                | Error Response | エンドポイントがオフラインになっているため、アクセスできなかったことを示します。 |
| [`UnsupportedOperationError`](#UnsupportedOperationError)  | Error Response | エンドポイントでサポートされないリクエストを示します。   |
| [`ValueOutOfRangeError`](#ValueOutOfRangeError)            | Error Response | エンドポイントが処理できる範囲外の値を設定しようとするリクエストを示します。 |

<div class="note">
<p><strong>メモ</strong></p>
<p>エラーメッセージの種類は追加される予定です。</p>
</div>

## ConditionsNotMetError {#ConditionsNotMetError}
エンドポイントが動作するための特定の条件(ステータス)が満たされていない場合、CEKにこのメッセージをレスポンスとして返します。CEKはこのメッセージを受け取ると、あらかじめ用意されたエラーメッセージをクライアントに送信します。

### Payload fields

なし

### 備考
* エラーが発生した場合にも、エラーメッセージはリクエスト成功のレスポンス(200 OK)でCEKに返す必要があります。
* エラーメッセージの名前で状況を判断するため、`payload`は必要ありません。

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

### 次の項目も参照してください。
* [`NotSupportedInCurrentModeError`](#NotSupportedInCurrentModeError)

## DeviceFailureError {#DeviceFailureError}
エンドポイントに障害が発生した場合、CEKにこのメッセージをレスポンスとして返します。CEKはこのメッセージを受け取ると、あらかじめ用意されたエラーメッセージをクライアントに送信します。

### Payload fields

なし

### 備考
* エラーが発生した場合にも、エラーメッセージはリクエスト成功のレスポンス(200 OK)でCEKに返す必要があります。
* エラーメッセージの名前で状況を判断するため、`payload`は必要ありません。

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

### 次の項目も参照してください。
* [`DriverInternalError`](#DriverInternalError)
* [`TargetOfflineError`](#TargetOfflineError)

## DriverInternalError {#DriverInternalError}
内部エラーが発生した場合、CEKにこのメッセージをレスポンスとして返します。CEKはこのメッセージを受け取ると、あらかじめ用意されたエラーメッセージをクライアントに送信します。

### Payload fields

なし

### 備考
* エラーが発生した場合にも、エラーメッセージはリクエスト成功のレスポンス(200 OK)でCEKに返す必要があります。
* エラーメッセージの名前で状況を判断するため、`payload`は必要ありません。

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

### 次の項目も参照してください。
* [`DeviceFailureError`](#DeviceFailureError)
* [`TargetOfflineError`](#TargetOfflineError)

## ExpiredAccessTokenError {#ExpiredAccessTokenError}
[アカウントリンク](/CEK/Guides/Link_User_Account.md)の際、[認可サーバー](/CEK/Guides/Link_User_Account.md#BuildAuthServer)から発行されたアクセストークンが期限切れである場合、CEKにこのメッセージをレスポンスとして返します。CEKはこのメッセージを受け取ると、あらかじめ用意されたエラーメッセージをクライアントに送信します。

### Payload fields

なし

### 備考
* エラーが発生した場合にも、エラーメッセージはリクエスト成功のレスポンス(200 OK)でCEKに返す必要があります。
* エラーメッセージの名前で状況を判断するため、`payload`は必要ありません。

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

### 次の項目も参照してください。
* [`InvalidAccessTokenError`](#InvalidAccessTokenError)

## InvalidAccessTokenError {#InvalidAccessTokenError}
ユーザーが使用中のアクセストークンに対する権限を解除した場合、CEKにこのメッセージをレスポンスとして返します。CEKはこのメッセージを受け取ると、あらかじめ用意されたエラーメッセージをクライアントに送信します。

### Payload fields

なし

### 備考
* エラーが発生した場合にも、エラーメッセージはリクエスト成功のレスポンス(200 OK)でCEKに返す必要があります。
* エラーメッセージの名前で状況を判断するため、`payload`は必要ありません。

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

### 次の項目も参照してください。
* [`ExpiredAccessTokenError`](#ExpiredAccessTokenError)

## NoSuchTargetError {#NoSuchTargetError}
エンドポイントが存在しない場合、このメッセージをレスポンスとして返します。例えば、ユーザーがIoTサービスから特定のデバイスを削除しましたが、そのことがClovaアプリにまだ反映されていない状態でそのデバイスの操作をリクエストされた場合、このメッセージを返します。CEKはこのメッセージを受け取ると、あらかじめ用意されたエラーメッセージをクライアントに送信します。

### Payload fields

なし

### 備考
* エラーが発生した場合にも、エラーメッセージはリクエスト成功のレスポンス(200 OK)でCEKに返す必要があります。
* エラーメッセージの名前で状況を判断するため、`payload`は必要ありません。

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

### 次の項目も参照してください。
* [`ConditionsNotMetError`](#ConditionsNotMetError)
* [`TargetOfflineError`](#TargetOfflineError)

## NotSupportedInCurrentModeError {#NotSupportedInCurrentModeError}
エンドポイントの現在のモードではサポートされないディレクティブを示します。例えば、エアコンの場合、除湿モードで動作している間は温度を調節できない製品があります。そのタイプのエアコンを使用しているユーザーが除湿モードで温度調節をリクエストした場合、このメッセージを返します。CEKはこのメッセージを受け取ると、あらかじめ用意されたエラーメッセージをクライアントに送信します。

### Payload fields

なし

### 備考
* エラーが発生した場合にも、エラーメッセージはリクエスト成功のレスポンス(200 OK)でCEKに返す必要があります。
* エラーメッセージの名前で状況を判断するため、`payload`は必要ありません。

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

### 次の項目も参照してください。
* [`UnsupportedOperationError`](#UnsupportedOperationError)
* [`ValueOutOfRangeError`](#ValueOutOfRangeError)

## TargetOfflineError {#TargetOfflineError}
エンドポイントがオフラインになっているため、アクセスできなかったことを示します。CEKはこのメッセージを受け取ると、あらかじめ用意されたエラーメッセージをクライアントに送信します。

### Payload fields

なし

### 備考
* エラーが発生した場合にも、エラーメッセージはリクエスト成功のレスポンス(200 OK)でCEKに返す必要があります。
* エラーメッセージの名前で状況を判断するため、`payload`は必要ありません。

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

### 次の項目も参照してください。
* [`DeviceFailureError`](#DeviceFailureError)
* [`DriverInternalError`](#DriverInternalError)

## UnsupportedOperationError {#UnsupportedOperationError}

エンドポイントでサポートされないリクエストを示します。ユーザーがエンドポイントでサポートされていない動作をリクエストした場合、CEKはすぐユーザーに有効な範囲外のリクエストであることを伝えます。ただし、`SetMode`のような動作は、Clova Home Extensionが[SetModeRequest](/CEK/References/ClovaHomeInterface/Control_Interfaces.md#SetModeRequest)メッセージを受信して`mode`フィールドの値を確認するまで、範囲内の動作かどうかを判断できません。もし、Clova Home Extensionがメッセージを受信し、サポートされていないモードである場合、エラーレスポンスを返す必要があります。その際、`UnsupportedOperationError`メッセージをCEKに返します。

例えば、ユーザーのサーモスタット(`"THERMOSTAT"`タイプ)が`SetMode`動作をサポートし、スリープモード(`"sleep"`)、外出モード(`"away"`)をサポートしている場合を仮定します。その場合、ユーザーがそのデバイスに冷房モード(`"cool"`)を設定するようにリクエストすると、Clova Home Extensionは`UnsupportedOperationError`メッセージをCEKに返す必要があります。

### Payload fields

なし

### 備考
* エラーが発生した場合にも、エラーメッセージはリクエスト成功のレスポンス(200 OK)でCEKに返す必要があります。
* エラーメッセージの名前で状況を判断するため、`payload`は必要ありません。

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

### 次の項目も参照してください。
* [`NotSupportedInCurrentModeError`](#NotSupportedInCurrentModeError)
* [`ValueOutOfRangeError`](#ValueOutOfRangeError)

## ValueOutOfRangeError {#ValueOutOfRangeError}
エンドポイントが処理できる範囲外の値を設定しようとするリクエストを受け取った場合、CEKにこのメッセージをレスポンスとして返します。例えば、エアコンが18から28までの設定温度の値をサポートしていて、ユーザーが16や30などの値を設定するようにリクエストした場合、このメッセージが返されます。`payload`にエンドポイントが処理できる最大値と最小値を含める必要があります。

### Payload fields

| フィールド名       | データ型    | フィールドの説明                     | 必須/選択 |
|---------------|---------|-----------------------------|:---------:|
| `maximumValue` | number | エンドポイントでサポートされる最大値 | 必須    |
| `minimumValue` | number | エンドポイントでサポートされる最小値 | 必須    |

### 備考
* エラーが発生した場合にも、エラーメッセージはリクエスト成功のレスポンス(200 OK)でCEKに返す必要があります。
* エラーメッセージの名前で状況を判断するため、`payload`は必要ありません。
* `payload`に入力された値は、ユーザーに設定値の有効範囲を案内する際に使用できます。

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

### 次の項目も参照してください。
* [`UnsupportedOperationError`](#UnsupportedOperationError)
* [`NotSupportedInCurrentModeError`](#NotSupportedInCurrentModeError)
