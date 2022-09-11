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
    fun generateShortUuid(): String {
        val uuid = UUID.randomUUID();
        val bb = ByteBuffer.wrap(ByteArray(16))
        bb.putLong(uuid.mostSignificantBits)
        bb.putLong(uuid.leastSignificantBits)
        val bytes = Base64.getUrlEncoder().encode(bb.array())
        return String(bytes);
    }
```
