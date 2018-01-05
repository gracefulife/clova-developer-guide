# Common objects

The content templates use the following JSON objects to represent commonly used data structures.
Each object has the `value` field for the actual data the object contains.
The `type` field defines the data type of the value.

| Object name            | Object description                                            |
|--------------------|---------------------------------------------------|
| [ActionObject](#ActionObject)             | Contains an action for the client to perform.          |
| [CurrencyObject](#CurrencyObject)         | Contains an amount of money with currency.               |
| [DateObject](#DateObject)                 | Contains a date                         |
| [DateTimeObject](#DateTimeObject)         | Contains a date and a time                    |
| [NumberObject](#NumberObject)             | Contains a number, separated by thousands |
| [PercentageObject](#PercentageObject)     | Contains a percentage.                        |
| [PhoneNumberObject](#PhoneNumberObject)   | Contains a phone number.                     |
| [StringObject](#StringObject)             | Contains text.                        |
| [TemperatureCObject](#TemperatureCObject) | Contains a temperature (Celsius).                    |
| [TemperatureFObject](#TemperatureFObject) | Contains a temperature (Fahrenheit).                    |
| [URLObject](#URLObject)                   | Contains a URL.                         |

# ActionObject {#ActionObject}

Contains an action for the client to perform.

### Object fields

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `type`          | string  | The value is always `"action"`.  |
| `value`         | string  | An action for the client to perform, in the form of [Action URL scheme](/CIC/References/ContentTemplates/Common_Fields.md#ActionURLScheme) |

### Object example

{% raw %}

```json
{
    "type": "action",
    "value": "clova://naverSearch?query=Brown%27sbirthday"
}
```

{% endraw %}

# CurrencyObject {#CurrencyObject}

Contains an amount of money with currency.

### Object fields

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `type`          | string  | The value is always `"currency"`.  |
| `value`         | string  | An amount of money with currency               |

### Object example

{% raw %}

```json
{
    "type": "currency",
    "value": "KRW500000"
}
```

{% endraw %}

## DateObject {#DateObject}

Contains a date.

### Object fields

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `type`          | string  | The value is always `"date"`.  |
| `value`         | string  | A date in YYYY-MM-DD   |

### Object example

{% raw %}

```json
{
    "type": "date",
    "value": "2017-05-29"
}
```

{% endraw %}

## DateTimeObject {#DateTimeObject}

Contains a date and a time.

### Object fields

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `type`          | string  | The value is always `"datetime"`.   |
| `value`         | string  | A date and a time in YYYY-MM-DDThh:mm:ssZ |

### Object example

{% raw %}

```json
{
    "type": "datetime",
    "value": "2017-07-26T18:00:00Z"
}
```

{% endraw %}

## NumberObject {#NumberObject}

Contains a number separated by thousands.

### Object fields

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `type`          | string  | The value is always `"number"`.    |
| `value`         | string  | A number separated by thousands |

### Object example

{% raw %}

```json
{
    "type": "number",
    "value": "19,304,213"
}
```

{% endraw %}

## PercentageObject {#PercentageObject}

Contains a percentage.

### Object fields

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `type`          | string  | The value is always `"percentage"`. |
| `value`         | number  | A percentage                         |

### Object example

{% raw %}

```json
{
    "type": "percentage",
    "value": 20.2341
}
```

{% endraw %}

## PhoneNumberObject {#PhoneNumberObject}

Contains a phone number.

### Object fields

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `type`          | string  | The value is always `"phoneNum"`. |
| `value`         | string  | A phone number                    |

### Object example

{% raw %}

```json
{
    "type": "phoneNum",
    "value": "031-784-1000"
}
```

{% endraw %}

## StringObject {#StringObject}

Contains text.

### Object fields

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `type`          | string  | The value is always `"string"`.  |
| `value`         | string  | Text                      |

### Object example

{% raw %}

```json
// Example 1
{
    "type": "string",
    "value": "Happy new year"
}

// Example 2
{
    "type": "string",
    "value": "NAVER search result"
}
```

{% endraw %}

## TemperatureCObject {#TemperatureCObject}

Contains a temperature in Celsius.

### Object fields

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `type`          | string  | The value is always `"temperature-c"`.   |
| `value`         | number  | A temperature in Celsius                      |

### Object example

{% raw %}

```json
{
    "type": "temperature-c",
    "value": 31
}
```

{% endraw %}

## TemperatureFObject {#TemperatureFObject}

Contains a temperature in Fahrenheit.

### Object fields

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `type`          | string  | The value is always `"temperature-f"`.   |
| `value`         | number  | A temperature in Fahrenheit                      |

### Object example

{% raw %}

```json
{
    "type": "temperature-f",
    "value": 75
}
```

{% endraw %}

## URLObject {#URLObject}

Contains a URL.

### Object fields

| Field name       | Type    | Description                     |
|---------------|:---------:|-----------------------------|
| `type`          | string  | The value is always `"url"`.   |
| `value`         | string  | A URL                        |

### Object example

{% raw %}

```json
// Example 1
{
    "type": "url",
    "value": "https://linecorp.com/ja/"
}

// Example 2
{
    "type": "url",
    "value": "https://www.linefriends.jp/search?query=cony%20pencil%20case"
}
```

{% endraw %}
