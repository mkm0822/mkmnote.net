---
title: "ディレクトリのファイル内の文字列を一括置換"
date: 2020-09-03T00:00:00+09:00
tags: [ bash ]
description: >
  ディレクトリのファイル内の文字列を一括置換するコマンドの例。

---

ディレクトリのファイル内の文字列を一括置換するコマンドの例です。
サブディレクトリも置換対象に含みます。

名前が `kustomization` で始まるファイルのうち，
パスに `base/` を含むファイル内の `deployment` という文字列を `resources` に置換するには以下のコマンドを実行します。

```
find . -name "kustomization*" | grep base/ | xargs sed -i -e 's/deployment/resources/g'
```

拡張子が `.yml` なファイルのうち，ファイル内に `yaml` という文字列を含むファイルの，
`yaml` という文字列を `yml` に置換するには以下のコマンドを実行します。。

```
find . -type f -name "*.yml" -print | xargs grep -l yaml | xargs sed -i "s/yaml/yml/g"
```
