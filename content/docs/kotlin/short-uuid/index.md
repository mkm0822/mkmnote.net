---
title: "Short UUID"
date: 2022-09-11T01:15:10+09:00
description: >
  短いUUID相当な文字列の作り方。

draft: true
---
ユニークかつ人間が読みやすいIDが欲しい場合，
UUIDを生成してそれをBase64でエンコードするのがお手頃でよい。

```kotlin
fun generateShortUuid() {
    Base64 base64 = new Base64();
    UUID uuid = UUID.fromString(str);
    ByteBuffer bb = ByteBuffer.wrap(new byte[16]);
    bb.putLong(uuid.getMostSignificantBits());
    bb.putLong(uuid.getLeastSignificantBits());
    return base64.encodeBase64URLSafeString(bb.array());
}
```
