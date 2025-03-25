---
author: Taro Gray
pubDatetime: 2025-03-25T22:00:00.000Z
title: jqはJSONデータを効率的に操作・抽出するための強力なコマンドラインツール
postSlug: linux-jq
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
  - jq
description: jqコマンドを使用すると、JSONデータから特定の条件に一致するエントリを簡単に抽出できます。特に、select関数を用いることで、複雑なフィルタリングも直感的に行うことが可能です。JSONデータを扱う際には、jqを活用して効率的なデータ操作を行いましょう。
---

## Table of contents

## jqは、JSONデータを効率的に操作・抽出するための強力なコマンドラインツール

特定の条件に基づいてデータをフィルタリングする際に非常に有用です。

以下のコマンドは、input.jsonファイル内のデータから、animeSeason.yearが2025であるエントリのみを抽出します：

```
jq '[.[] | select(.animeSeason.year == 2025)]' input.json
```

このコマンドの構造と動作を詳しく見ていきましょう。

コマンドの構造1. jqコマンド：JSONデータを処理するためのツールです。2. [.[] | select(.animeSeason.year == 2025)]：jqに対するフィルタ式で、以下の部分から成り立っています：- .[]：入力されたJSON配列の各要素に対して処理を行います。- select(.animeSeason.year == 2025)：各要素の中で、animeSeasonオブジェクトのyearプロパティが2025であるものを選択します。- [...]：選択された要素を新しい配列としてまとめます。3. input.json：処理対象のJSONファイル名です。 ￼

### JSONファイルの準備

まず、以下のようなJSONデータをinput.jsonというファイル名で保存します：

```
[
  {
    "sources": [
      "https://anilist.co/anime/142051",
      "https://anime-planet.com/anime/raise-a-suilen-nvade-show"
    ],
    "title": "!NVADE SHOW!",
    "type": "SPECIAL",
    "episodes": 1,
    "status": "FINISHED",
    "animeSeason": {
      "season": "FALL",
      "year": 2025
    }
  },
  {
    "sources": [
      "https://anidb.net/anime/10143",
      "https://anilist.co/anime/102416"
a    ],
    "title": "\"0\"",
    "type": "SPECIAL",
    "episodes": 1,
    "status": "FINISHED",
    "animeSeason": {
      "season": "SUMMER",
      "year": 2013
    }
  }
]
```

### コマンドの実行

ターミナルで以下のコマンドを実行します：

```
jq '[.[] | select(.animeSeason.year == 2025)]' input.json
```

このコマンドは、input.json内の各オブジェクトを評価し、animeSeason.yearが2025であるものを抽出して新しい配列として出力します。

出力結果

```
[
  {
    "sources": [
      "https://anilist.co/anime/142051",
      "https://anime-planet.com/anime/raise-a-suilen-nvade-show"
    ],
    "title": "!NVADE SHOW!",
    "type": "SPECIAL",
    "episodes": 1,
    "status": "FINISHED",
    "animeSeason": {
      "season": "FALL",
      "year": 2025
    }
  }
]
```

このように、animeSeason.yearが2025のエントリのみが抽出されます。

### ファイルパスの指定

input.jsonが現在の作業ディレクトリ以外にある場合、フルパスまたは相対パスを指定する必要があります。例えば：

```
jq '[.[] | select(.animeSeason.year == 2025)]' /path/to/input.json
```

標準入力からのデータ処理

ファイルを使用せず、直接JSONデータをコマンドに渡す場合は、echoコマンドとパイプを使用します：

```
echo '[{"animeSeason": {"year": 2025}}, {"animeSeason": {"year": 2013}}]' | jq '[.[] | select(.animeSeason.year == 2025)]'
```

この方法では、直接JSONデータを入力として処理できます。

### まとめ

jqコマンドを使用すると、JSONデータから特定の条件に一致するエントリを簡単に抽出できます。特に、select関数を用いることで、複雑なフィルタリングも直感的に行うことが可能です。JSONデータを扱う際には、jqを活用して効率的なデータ操作を行いましょう。
