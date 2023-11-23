---
author: Taro Gray
pubDatetime: 2023-11-16T12:05:00.00Z
title: 【terminalコマンドの基本】WindowsのツリーコマンドをMacで
postSlug: mac-tree-terminal
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Mac
  - tree
  - terminal
  - command
  - linux
description: MacOSにはデフォルトで「tree」コマンドがインストールされていないため、代替方法を使用するか、Homebrewなどのパッケージマネージャーを使用してインストールする必要があります。
---

## Table of contents

MacOSにはデフォルトで「tree」コマンドがインストールされていないため、代替方法を使用するか、Homebrewなどのパッケージマネージャーを使用してインストールする必要があります。

## 代替方法

Macのターミナルでディレクトリ構造を表示するには、以下のコマンドを使用できます。

```bash
find . -print | sed -e 's;[^/]*/;|____;g;s;____|; |;g'
```

このコマンドは現在のディレクトリ以下のすべてのファイルとディレクトリを表示し、階層構造を視覚的に表現します。

## Homebrewを使用したtreeコマンドのインストール

もしHomebrewがインストールされている場合は、以下のコマンドで「tree」をインストールできます。

```bash
brew install tree
```

インストール後、通常の「tree」コマンドと同様に使用できます。例えば、以下のコマンドで現在のディレクトリの構造を表示できます。

```bash
tree
```

これらの方法でMac上でディレクトリの構造を確認することができます。
