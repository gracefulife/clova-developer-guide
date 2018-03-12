{% if book.TargetCountryCode == "KR" %}

Clovaは、以下のオーディオ圧縮フォーマットに対応しています。

| オーディオ圧縮フォーマット        | ファイル拡張子 | 配信方式                 | ライセンス費用 |
|----------------------------------|:--------:|-------------------------------|-----------|
| MPEG-1 or MPEG-2 Audio Layer III | .mp3     | HLS(HTTP Live Streaming) v3   | 無料     |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clovaが対応するオーディオ圧縮フォーマットと配信方式は、さらに増える可能性があります。</p>
</div>

{% elif book.TargetCountryCode == "JP" %}

Clovaは、以下のオーディオ圧縮フォーマットに対応しています。

| オーディオ圧縮フォーマット        | ファイル拡張子 | 配信方式                 | ライセンス費用 |
|----------------------------------|:--------:|-------------------------------|-----------|
| Advanced Audio Coding            | .aac     | HLS(HTTP Live Streaming) v3   | 有料     |
| MPEG-1 or MPEG-2 Audio Layer III | .mp3     | HLS(HTTP Live Streaming) v3   | 無料     |

<div class="note">
  <p><strong>Note!</strong></p>
  <p>Clovaが対応するオーディオ圧縮フォーマットと配信方式は、さらに増える可能性があります。なお、有料オーディオ圧縮フォーマットの音源を再生する場合、ライセンス費用の支払いを求められることがあります。ライセンス費用の詳細については、提携担当者まで別途お問い合わせください。</p>
</div>

{% endif %}
