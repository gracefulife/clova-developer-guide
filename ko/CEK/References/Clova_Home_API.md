# Clova Home API

IoT 기기를 제어할 때 사용하는 API이며, 메시지 헤더(`header`)의 값으로 **"ClovaHome"**을 가집니다. Clova Home extension은 이 API를 사용하여 제어할 수 있는 기기 목록을 제공하거나 사용자가 등록한 IoT 기기를 제어해야 합니다. Clova Home API는 다음과 같이 분류됩니다.

* [Discovery API](#DiscoveryAPI)
* [Control API](#ControlAPI)
* [Error API](#ErrorAPI)
* [Shared objects](#SharedObjects)

{% include "./ClovaHomeAPI/Discovery_API.md" %}

{% include "./ClovaHomeAPI/Control_API.md" %}

{% include "./ClovaHomeAPI/Error_API.md" %}

{% include "./ClovaHomeAPI/Shared_Objects.md" %}
