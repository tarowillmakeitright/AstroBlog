---
author: Taro Gray
pubDatetime: 2024-04-27T15:25:00.00Z
title: Vim でのテキスト置換完全ガイド
postSlug: neovim-text-replacement
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Neovim
  - text replacement
description: Vim はその強力なテキスト編集機能で知られていますが、その中でも特に有用なのが「置換」機能です。この記事では、Vim での基本的な置換から複雑なパターンを使った置換まで、詳細にわたって説明します。
---

## Table of contents

## 基本的な置換

Vim での最も基本的な置換コマンドは次の形式を取ります：

```vim
:[範囲]s/検索パターン/置換文字列/フラグ
```

ここでの要素は以下の通りです：

- **範囲**：置換を適用する行の範囲。省略した場合、現在の行だけが対象となります。
- **検索パターン**：置換したいテキストのパターン。
- **置換文字列**：新しいテキスト。
- **フラグ**：置換の挙動を制御するオプション（例：`g`は全グローバル置換）。

### 例：

全ての行で "hello" を "world" に置換するには、以下のコマンドを使用します。

```vim
:%s/hello/world/g
```

## 範囲指定の置換

特定の行範囲内での置換を行う場合、行番号やパターンを使って範囲を指定します。

### 例：

10行目から20行目までで "apple" を "orange" に置換する場合は、以下のようにします。

```vim
:10,20s/apple/orange/g
```

## 置換のフラグ

Vim の置換機能には、操作をカスタマイズするためのいくつかのフラグがあります。

- `g` - 行内の全てのインスタンスを置換します。
- `c` - 置換を行う前に確認を求めます。
- `i` - 大文字と小文字を区別せずに置換します。

## 高度な置換

正規表現を使用すると、より複雑なテキストパターンを置換できます。例えば、数字を含む文字列を置換したい場合は以下のようにします。

```vim
:%s/foo\d+/bar/g
```

## 関連記事とリソース

Vim の置換機能についてさらに学びたい場合、以下のリソースが役立ちます：

- [Vim documentation](https://www.vim.org/docs.php) - Vim の公式ドキュメントは、多くの機能とコマンドの詳細を提供しています。
- [Practical Vim](https://pragprog.com/titles/dnvim2/practical-vim-second-edition/) - Drew Neil の著書で、Vim の使い方を実用的な観点から解説しています。
