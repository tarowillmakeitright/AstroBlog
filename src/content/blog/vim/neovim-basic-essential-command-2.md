---
author: Taro Gray
pubDatetime: 2024-01-27T20:47:00.00Z
title: Neovim入門：基本的なコマンドとテクニック 第２章
postSlug: neovim-basic-essential-command-2
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Neovim
  - neovim basic essential command
description: この記事はNeovimの基本操作といくつかの便利なコマンドを紹介することで、日常のコーディング作業の効率化に役立つことを目指しています。次のパートでは、さらに高度な機能とテクニックに焦点を当てていきます。
---

## Table of contents

## Neovim入門：基本的なコマンドとテクニック

NeovimはVimの強化版で、多くの開発者に愛用されている強力なテキストエディタです。このブログでは、Neovimの基本コマンドといくつかの応用テクニックを紹介します。ここでは中級者向けに、日常的な作業を効率化するコマンドをいくつか取り上げます。

## コピーやペースト、削除

1. **ペースト (`p`)**: レジスタに保存されているテキストを現在のカーソル位置にペーストします。
2. **コピー (`yy`)**: 現在の行をコピーしてレジスタに保存します。
3. **削除 (`dd`)**: 現在の行を削除し、削除した内容をレジスタに保存します。

## 編集と変更

1. **一文字削除 (`x`)**: カーソル位置の文字を削除します。
2. **単語削除 (`dw`)**: カーソル位置から単語の終わりまで削除します。
3. **行の連結 (`J`)**: 現在の行と次の行を結合します。

## 移動と検索

1. **行番号表示 (`:set number`)**: 各行の行番号を表示します。
2. **特定の行へ移動 (`:10`)**: 10行目にカーソルを移動します。
3. **文書内検索 (`/`)**: 文書内で文字列を検索します。
4. **次の検索結果へ (`n`), 前の検索結果へ (`N`)**: 検索結果を順に移動します。

## インデントと整形

1. **右インデント (`>`)**: 選択範囲を右にインデントします。
2. **左インデント (`<`)**: 選択範囲を左にインデントします。

## マクロと自動化

1. **行頭にコメント追加 (`:norm I #`)**: 各行の始めに `#` を挿入します。
2. **行末にコメント追加 (`:norm A #`)**: 各行の末尾に `#` を追加します。

## プラグインと拡張機能

1. **NERDTree**: ファイルとディレクトリをツリー形式で表示するプラグインです。
2. **fzf**: 強力なファジーファインダーで、ファイルやコマンド履歴などを素早く検索できます。

## 参考文献とリンク

- [Neovim公式サイト](https://neovim.io/)
- [Practical Vim](https://pragprog.com/titles/dnvim2/practical-vim-second-edition/): Vimを使いこなすための実用的なガイド。