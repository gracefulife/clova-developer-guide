{% if book.TargetCountryCode == "KR" %}

Audio compression formats supported by Clova are as follows:

| Audio compression format                     | File extension | Transmission protocol                       | License cost |
|----------------------------------|:--------:|-------------------------------|-----------|
| MPEG-1 or MPEG-2 Audio Layer III | .mp3     | HTTP Live Streaming (HLS) v3   | Free       |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>There may be further support in the future for audio compression formats and transmission protocols by Clova.</p>
</div>

{% elif book.TargetCountryCode == "JP" %}

Audio compression formats supported by Clova are as follows:

| Audio compression format                     | File extension | Transmission protocol                       | License cost |
|----------------------------------|:--------:|-------------------------------|-----------|
| Advanced Audio Coding            | .aac     | HTTP Live Streaming (HLS) v3   | Paid       |
| MPEG-1 or MPEG-2 Audio Layer III | .mp3     | HTTP Live Streaming (HLS) v3   | Free       |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>There may be further support in the future for audio compression formats and transmission protocols by Clova. Also, a license cost may be incurred for playing music that is in the audio compression format of a paid service. Please contact the Partnership Manager for details on license fees.</p>
</div>

{% endif %}
