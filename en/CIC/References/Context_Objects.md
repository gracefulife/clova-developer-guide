# Context information

A context is a state of a client and is specified in context objects. Context objects are included in the [events](/CIC/References/CIC_API.md#Event) sent to CIC. Context objects shall contain the state at the point of user's voice request. The following is available context objects:

* [`Alerts.AlertsState`](#AlertsState)
* [`AudioPlayer.PlaybackState`](#PlaybackState)
* [`Device.DeviceState`](#DeviceState)
* [`Device.Display`](#Display)
* [`Clova.Location`](#Location)
* [`Clova.SavedPlace`](#SavedPlace)
* [`Speaker.VolumeState`](#VolumeState)

{% include "/CIC/References/ContextObjects/AlertsState.md" %}

{% include "/CIC/References/ContextObjects/PlaybackState.md" %}

{% include "/CIC/References/ContextObjects/DeviceState.md" %}

{% include "/CIC/References/ContextObjects/Display.md" %}

{% include "/CIC/References/ContextObjects/Location.md" %}

{% include "/CIC/References/ContextObjects/SavedPlace.md" %}

{% include "/CIC/References/ContextObjects/VolumeState.md" %}
