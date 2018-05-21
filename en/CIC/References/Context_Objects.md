# Context

A context is a state of a client and is specified in context objects. Context objects are included in the [events](/CIC/References/CIC_API.md#Event) sent to CIC. Context objects contain the device state at the time of a user voice request. The available context objects are as follows:

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
