# Context information

A context is a state of a client and is specified in context objects. Context objects are included in the [events](/CIC/References/CIC_API.md#Event) sent to CIC. Context objects shall contain the state at the point of user's voice request. The following is available context objects:

* [`Alerts.AlertsState`](#AlertsState)
* [`AudioPlayer.PlaybackState`](#PlaybackState)
* [`Device.DeviceState`](#DeviceState)
* [`Device.Display`](#Display)
* [`Clova.Location`](#Location)
* [`Clova.SavedPlace`](#SavedPlace)
* [`Speaker.VolumeState`](#VolumeState)

{% include "./ContextObjects/AlertsState.md" %}

{% include "./ContextObjects/PlaybackState.md" %}

{% include "./ContextObjects/DeviceState.md" %}

{% include "./ContextObjects/Display.md" %}

{% include "./ContextObjects/Location.md" %}

{% include "./ContextObjects/SavedPlace.md" %}

{% include "./ContextObjects/VolumeState.md" %}
