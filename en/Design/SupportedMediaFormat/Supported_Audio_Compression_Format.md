{% if book.language == "KR" %}

Audio compression formats supported by Clova are as follows:

| Audio Compression Format                     | File Extension | Transmission Method                       | License Cost |
|----------------------------------|:--------:|-------------------------------|-----------|
| MPEG-1 or MPEG-2 Audio Layer III | .mp3     | HTTP Live Streaming (HLS) v3   | Free       |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>There may be further support in the future for audio compression formats and transmission methods by Clova.</p>
</div>

{% elif book.language == "JP" %}

Audio compression formats supported by Clova are as follows:

| Audio Compression Name                     | File Extension | Transmission Method                       | License Cost |
|----------------------------------|:--------:|-------------------------------|-----------|
| Advanced Audio Coding            | .aac     | HTTP Live Streaming (HLS) v3   | Paid       |
| MPEG-1 or MPEG-2 Audio Layer III | .mp3     | HTTP Live Streaming (HLS) v3   | Free       |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>There may be further support in the future for audio compression formats and transmission methods by Clova. Also, a license cost may be incurred for playing music that is in the audio compression format of a paid service. Please contact the Partner Manager for details on license fees.</p>
</div>

{% endif %}
