# Context information

Context indicates various states information of a client. Context information is included in a context object which is sent with an [Event message](/CIC/References/CIC_Message_Format.md#Event) of the CIC APIs. Context should contain states information at the time when user's speech input is initiated. Available context objects are as follows.

* [AudioPlayer.PlaybackState](#PlaybackState)
* [Device.DeviceState](#DeviceState)
* [Clova.FreetalkState](#FreetalkState)
* [Clova.Location](#Location)
* [Clova.SavedPlace](#SavedPlace)
* [Speaker.VolumeState](#VolumeState)

{% include "./ContextObjects/PlaybackState.md" %}

{% include "./ContextObjects/DeviceState.md" %}

{% include "./ContextObjects/FreetalkState.md" %}

{% include "./ContextObjects/Location.md" %}

{% include "./ContextObjects/SavedPlace.md" %}

{% include "./ContextObjects/VolumeState.md" %}