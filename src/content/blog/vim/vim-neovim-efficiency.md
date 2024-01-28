---
author: Taro Gray
pubDatetime: 2024-01-27T21:02:00.00Z
title: Neovimでの効率的なテキスト編集とナビゲーション
postSlug: vim-neovim-efficiency
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Neovim
description: この記事では、Neovimの基本から応用までのコマンドを紹介しました。これらのコマンドをマスターすることで、日々のテキスト編集作業をより効率的に進めることができます。
---

## Table of contents

## Neovimでの効率的なテキスト編集とナビゲーション

Neovimは、その強力な編集機能と柔軟なカスタマイズオプションで高く評価されています。この記事では、Neovimでの効率的なテキスト操作とナビゲーションの方法に焦点を当て、中級者向けの具体的なコマンド例を紹介します。

## 移動コマンド

- **指定行への移動**: `:10` で10行目にジャンプ。
- **行末への移動**: `$` で現在の行の末尾に移動。
- **行頭への移動**: `0` で行の先頭に移動。
- **インデントの先頭へ**: `^` で現在の行の最初の非空白文字に移動。
- **段落のナビゲーション**: `(` と `)` で上下の段落に移動。
- **セクションのナビゲーション**: `[[` と `]]` で上下のセクションに移動。
- **ファイルの先頭へ**: `gg` で文書の先頭に移動。
- **前の位置に戻る**: `Ctrl + o` で以前の位置に戻る。

## 検索と置換

- **文書内検索**: `/keyword` でキーワードを検索。
- **検索結果のナビゲーション**: `n` で次の検索結果、`N` で前の検索結果に移動。
- **一括置換**: `:%s/old/new/g` で全ての `old` を `new` に置換。

## 編集と整形

- **行の連結**: `J` で次の行を現在の行に結合。
- **インデントの調整**: `>` と `<` で選択範囲のインデントを右左に調整。
- **ビジュアルモード**: `v` でテキストを選択して操作。

## プラグインと拡張機能

- **NERDTree**: ディレクトリとファイルのツリー表示を提供。
- **fzf**: ファジーファインダーを使用した高速なファイル検索。
- **vim-gitgutter**: 編集中のファイルに対するGitの変更点を表示。

## コマンドラインツールとの統合

- **ファイル検索**: `find . -name models.py | fzf` で `models.py` を検索。
- **ファイル削除**: `find . -name '*.pyc' | xargs rm` で `.pyc` ファイルを一括削除。
- **ファイル中のキーワード検索**: `grep "test" -nr` で `test` を含む行を検索。

## ナビゲーションとプロセス管理

- **ディレクトリ履歴の管理**: `pushd` と `popd` でディレクトリ間を移動。
- **プロセスの終了**: `ps aux | grep a.py | grep -v grep | awk '{print $2}' | xargs kill -9` で特定のプロセスを終了。