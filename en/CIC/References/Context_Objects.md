# Context information

Context information indicates various states of a client. To provide context, include context objects when sending [event messages](/CIC/References/CIC_API.md#Event) (CIC APIs). Context information must reflect states at the time when the user has spoken. The following are the available context objects.

* [`Alerts.AlertsState`](#AlertsState)
* [`AudioPlayer.PlaybackState`](#PlaybackState)
* [`Device.DeviceState`](#DeviceState)
* [`Device.Display`](#Display)
* [`Clova.FreetalkState`](#FreetalkState)
* [`Clova.Location`](#Location)
* [`Clova.SavedPlace`](#SavedPlace)
* [`Speaker.VolumeState`](#VolumeState)

{% include "./ContextObjects/AlertsState.md" %}

{% include "./ContextObjects/PlaybackState.md" %}

{% include "./ContextObjects/DeviceState.md" %}

{% include "./ContextObjects/Display.md" %}

{% include "./ContextObjects/FreetalkState.md" %}

{% include "./ContextObjects/Location.md" %}

{% include "./ContextObjects/SavedPlace.md" %}

{% include "./ContextObjects/VolumeState.md" %}