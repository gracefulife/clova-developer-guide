# 맥락 정보(Context)

맥락 정보(Context)는 클라이언트의 다양한 상태 정보를 의미합니다. 맥락 정보는 context objects를 통해 표현되며, CIC의 API인 [이벤트 메시지](/CIC/References/CIC_API.md#Event)를 보낼 때 포함됩니다. 맥락 정보는 사용자가 발화한 시점의 상태 정보를 담아야 하며, 다음과 같은 context objects가 있습니다.

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
