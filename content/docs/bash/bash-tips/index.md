---
title: "Bash Tips"
date: 2020-09-03T00:00:00+09:00
weight: 1
tags: [ "bash" ]
description: >
  BashのTipsです。

---

## 複数bashプロセス間でhistoryを共有

複数のbashプロセス間でhistoryを共有するには `.bashrc` に以下の設定を記述します。

```
PROMPT_COMMAND="history -a; history -c; history -r; $PROMPT_COMMAND"
shopt -u histappend
```

一行目で，コマンド履歴をファイルに追記，メモリ上のコマンド履歴を消去，コマンド履歴をファイルから読み込み，という処理をコマンドを実行するたびに実行するように設定しています。

二行目ではbashを修了したときにコマンド履歴をhistoryファイルに書き込まないように指定しています。

## サブディレクトリのファイル内の文字列を一括置換

サブディレクトリのファイル内の文字列をを一括置換するコマンドの例です。

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

## 標準出力と標準エラーの両方を捨てる

コマンドの実行したときの標準出力と標準エラーを両方捨てるには以下のようにリダイレクトします。

```
cmd > /dev/null 2>&1
```

## 文字列を含むか判定

ある文字列にある文字列が含まれるかを判定するには以下のように `if` を記述します。

```sh
STR='GNU/Linux is an operating system'
SUB='Linux'
if [[ "$STR" == *"$SUB"* ]]; then
  echo "It's there."
fi
```
## OSの判定

OSを判定するには `uname` コマンドを使います。

```sh
if [[ "$(uname)" == *'Linux'* ]]; then
    echo "linux"
elif [[ "$(uname)" == *'Darwin* ]]; then
    echo "mac"
elif [[ "$(uname)" == *'MINGW64'* ]]; then
    echo "win"
fi
```

## 変数の空文字判定

変数が空文字かを判定するには以下のように `if` を記述します。
変数を""で囲む必要があることに注意。

STRING変数が空または空文字でないかどうか。

```bash
if [ -n "$STRING" ]; then
  # 空でないときの処理
fi
```

STRING変数が空または空文字かどうか。

```bash
if [ -z "$STRING" ]; then
  # 空のときの処理
fi
```

## 変数の大文字化/小文字化

変数の大文字化または小文字化。

| 記述     | 説明                    | 例                             |
| -------- | ---------------------- | ------------------------------ |
| `${v^}`  | 大文字化(１文字目のみ)  | `v="ho ge"; echo ${v^}`→Ho ge  |
| `${v^^}` | 大文字化(全文字)        | `v="ho ge"; echo ${v^^}`→HO GE |
| `${v,}`  | 小文字化(１文字目のみ)  | `v="HO GE"; echo ${v,}`→hO GE  |
| `${v,,}` | 小文字化(全文字)        | `v="HO GE"; echo ${v,,}`→ho ge |
| `${v~}`  | 大小反転(１文字目のみ※) | `v="ho GE"; echo ${v~}`→Ho gE  |
| `${v~~}` | 大小反転(全文字)        | `v="ho GE"; echo ${v~~}`→HO GE |

## コマンド補完時に大文字小文字を区別しない

`.inputrc` に以下を追加します。

```
set completion-ignore-case on
```
