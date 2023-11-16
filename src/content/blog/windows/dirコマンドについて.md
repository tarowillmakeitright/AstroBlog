---
author: LIL JAP KID
pubDatetime: 2023-11-16T12:11:00.000Z
title: 【cmdコマンドの基本】MacのlsコマンドをWindowsで 
postSlug: dirコマンドについて
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Windows
  - dir
  - cmd 
  - command
  - linux
description: "ファイルがどこにあるかを確認するために、コマンドライン（コマンドプロンプトまたはターミナル）を使用して、`dir`コマンド（Windowsの場合）または`ls`コマンド（Unix/Linuxの場合）を使います。そして、ファイル名を指定して検索を行います。
"
---

## Table of contents

ファイルがどこにあるかを確認するために、コマンドライン（コマンドプロンプトまたはターミナル）を使用して、`dir`コマンド（Windowsの場合）または`ls`コマンド（Unix/Linuxの場合）を使います。そして、ファイル名を指定して検索を行います。

Windowsの場合（`dir`コマンドを使用）:

```
dir /s /b "ファイル名"
```

Unix/Linuxの場合（`ls`コマンドを使用）:

```
find / -name "ファイル名" 2>/dev/null
```

上記のコマンドの概要を説明します：

- `/s`（Windowsの場合）: 指定したディレクトリ以下のすべてのサブディレクトリを検索します。
- `/b`（Windowsの場合）: ファイル名だけを表示し、詳細な情報を省略します。
- `find`（Unix/Linuxの場合）: ファイルを検索するコマンドです。
- `/`（Unix/Linuxの場合）: ルートディレクトリから検索を開始します。
- `-name`（Unix/Linuxの場合）: ファイル名を指定します。
- `2>/dev/null`（Unix/Linuxの場合）: エラーメッセージを/dev/nullにリダイレクトし、エラー出力を無視します。

これらのコマンドを使って、指定したファイル名を持つファイルの場所を検索できます。ただし、WindowsとUnix/Linuxでコマンドが異なるため、適切な環境に合わせて選択してください。また、検索に時間がかかることがあるので、大規模なファイルシステムを検索する場合はお待ちいただくか、より具体的なディレクトリを指定して検索を制限することをお勧めします。
