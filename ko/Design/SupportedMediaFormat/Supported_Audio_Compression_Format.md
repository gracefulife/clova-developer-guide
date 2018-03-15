{% if book.TargetCountryCode == "KR" %}

Clova가 지원하는 오디오 압축 포맷은 다음과 같습니다.

| 오디오 압축 포맷                     | 파일 확장자 | 전송 방식                       | 라이선스 비용 |
|----------------------------------|:--------:|-------------------------------|-----------|
| MPEG-1 or MPEG-2 Audio Layer III | .mp3     | HLS(HTTP Live Streaming) v3   | 무료       |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova가 지원하는 오디오 압축 포맷과 전송 방식은 더 늘어날 수 있습니다.</p>
</div>

{% elif book.TargetCountryCode == "JP" %}

Clova가 지원하는 오디오 압축 포맷은 다음과 같습니다.

| 오디오 압축 포맷                     | 파일 확장자 | 전송 방식                       | 라이선스 비용 |
|----------------------------------|:--------:|-------------------------------|-----------|
| Advanced Audio Coding            | .aac     | HLS(HTTP Live Streaming) v3   | 유료       |
| MPEG-1 or MPEG-2 Audio Layer III | .mp3     | HLS(HTTP Live Streaming) v3   | 무료       |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clova가 지원하는 오디오 압축 포맷과 전송 방식은 더 늘어날 수 있습니다. 또한 유료의 오디오 압축 포맷으로 된 음원을 재생해야 하는 경우 라이선스 비용을 지불해야 할 수 있습니다. 라이선스 비용과 관련된 자세한 내용은 제휴 담당자에게 별도 문의하시기 바랍니다.</p>
</div>

{% endif %}
