# Clova Home API

This API controls IoT appliances. Its message header (`header`) is set to **"ClovaHome"**. Your Clova Home extension uses this API to provide a list of controllable appliances or to control IoT appliances registered to a user. The Clova Home API is divided into following APIs.

* [Discovery API](#DiscoveryAPI)
* [Control API](#ControlAPI)
* [Error API](#ErrorAPI)
* [Shared objects](#SharedObjects)

{% include "./ClovaHomeAPI/Discovery_API.md" %}

{% include "./ClovaHomeAPI/Control_API.md" %}

{% include "./ClovaHomeAPI/Error_API.md" %}

{% include "./ClovaHomeAPI/Shared_Objects.md" %}