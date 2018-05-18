# コンテキスト

コンテキストは、クライアントのさまざまな状態を示します。コンテキストオブジェクトで表され、CIC APIの[イベント](/CIC/References/CIC_API.md#Event)を送信する際に含まれます。コンテキストは、ユーザーが発話した時点の状態情報を持っている必要があります。コンテキストオブジェクトは次のようなものがあります。

* [`Alerts.AlertsState`](#AlertsState)
* [`AudioPlayer.PlaybackState`](#PlaybackState)
* [`Clova.Location`](#Location)
* [`Clova.SavedPlace`](#SavedPlace)
* [`Device.DeviceState`](#DeviceState)
* [`Device.Display`](#Display)
* [`Speaker.VolumeState`](#VolumeState)
* [`SpeechSynthesizer.SpeechState`](#SpeechState)

{% include "/CIC/References/ContextObjects/AlertsState.md" %}

{% include "/CIC/References/ContextObjects/PlaybackState.md" %}

{% include "/CIC/References/ContextObjects/Location.md" %}

{% include "/CIC/References/ContextObjects/SavedPlace.md" %}

{% include "/CIC/References/ContextObjects/DeviceState.md" %}

{% include "/CIC/References/ContextObjects/Display.md" %}

{% include "/CIC/References/ContextObjects/VolumeState.md" %}

{% include "/CIC/References/ContextObjects/SpeechState.md" %}
