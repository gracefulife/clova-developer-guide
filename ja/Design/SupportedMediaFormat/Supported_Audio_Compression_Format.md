{% if book.TargetCountryCode == "KR" %}

Clovaでは、以下の音声圧縮形式がサポートされています。

| 音声圧縮形式                     | ファイルの拡張子 | 転送方式                       | ライセンス費用 |
|----------------------------------|:--------:|-------------------------------|-----------|
| MPEG-1 or MPEG-2 Audio Layer III | .mp3     | HLS(HTTP Live Streaming) v3   | 無料       |

<div class="note">
  <p><strong>メモ</strong></p>
  <p>Clovaでサポートされている音声圧縮形式と転送方式は、さらに増える可能性があります。</p>
</div>

{% elif book.TargetCountryCode == "JP" %}

Clovaでは、以下の音声圧縮形式がサポートされています。

| 音声圧縮形式                     | ファイルの拡張子 | 転送方式                       | ライセンス費用 |
|----------------------------------|:--------:|-------------------------------|-----------|
| Advanced Audio Coding            | .aac     | HLS(HTTP Live Streaming) v3   | 有料       |
| MPEG-1 or MPEG-2 Audio Layer III | .mp3     | HLS(HTTP Live Streaming) v3   | 無料       |

<div class="note">
  <p><strong>メモ</strong></p>
  <p>Clovaでサポートされている音声圧縮形式と転送方式は、さらに増える可能性があります。また、有料の音声圧縮形式のオーディオを再生する場合、ライセンス費用を支払うことがあります。ライセンス費用に関する詳細は、提携担当者までお問い合わせください。</p>
</div>

{% endif %}
