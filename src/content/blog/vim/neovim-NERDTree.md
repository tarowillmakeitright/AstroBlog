---
author: Taro Gray
pubDatetime: 2024-04-10T22:15:00.00Z
title: NERDTreeの基本コマンド
postSlug: neovim-NERDTree
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Neovim
  - NERDTree
description: NERDTreeはVimでのプロジェクト管理を大きく改善するプラグインです。このガイドがNERDTreeの基本的な使用方法の理解に役立つことを願っています。
---

## Table of contents

NERDTreeは、Vimでファイルやディレクトリの構造を視覚的に表示し、操作できるようにするプラグインです。これにより、プロジェクトのナビゲーションが容易になります。

## インストール

NERDTreeは、Vimのプラグインマネージャー（例えば、`Vundle`, `vim-plug`など）を通じて簡単にインストールできます。`vim-plug`を使用している場合、以下の手順でインストールできます。

1. `.vimrc`ファイルまたは`init.vim`ファイルに以下を追加します。

   ```vim
   Plug 'preservim/nerdtree'
   ```

2. Vimを開き、`:PlugInstall`コマンドを実行します。

## 基本コマンド

- **NERDTreeの起動**: Vimで`NERDTree`を起動するには、`:NERDTree`コマンドを実行します。
- **ツリーの表示/非表示**: ツリーを表示または非表示にするには、`Ctrl + n`（デフォルトのキーバインド）を使用します。
- **ディレクトリの開閉**: ディレクトリを開くには、カーソルをディレクトリに移動し、`o`キーを押します。同様に、ディレクトリを閉じるには、`x`キーを使用します。
- **ファイルの開き方**: ファイルを開くには、カーソルをファイルに移動し、`o`キーを押します。新しいタブでファイルを開くには、`t`キーを使用します。
- **ノードの追加と削除**: ディレクトリやファイルを追加するには、`m`キーを押した後に表示されるメニューから選択します。削除するには、同様に`m`キーを押し、メニューから削除オプションを選択します。
- **リフレッシュ**: NERDTreeのビューをリフレッシュするには、`r`キーを押します。親ディレクトリをリフレッシュするには、`R`キーを使用します。

## 設定のカスタマイズ

`.vimrc`ファイルまたは`init.vim`ファイルでNERDTreeの挙動をカスタマイズできます。例えば、NERDTreeをVim起動時に自動的に表示させたい場合は、以下を追加します。

```vim
autocmd vimenter * NERDTree
```
