---
author: Taro Gray
pubDatetime: 2024-01-27T20:47:00.00Z
title: TMUXでVimのようにテキストをコピー＆ペーストする方法
postSlug: neovim-tmux-copy
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Neovim
  - tmux copy
description: TMUXは、複数のウィンドウを1つの物理的なターミナル内で扱うことができる非常に強力なツールです。プログラマーやシステム管理者にとっては、日常的な作業をより効率的に行うために欠かせないツールの一つです。今回は、TMUX上でVimのキーバインドを利用してテキストをコピー＆ペーストする方法をご紹介します。
---

## Table of contents

## ステップ1: TMUXを起動する

まずは、ターミナルを開き、次のコマンドでTMUXを起動します。

```bash
tmux
```

## ステップ2: キーバインドの設定

TMUXでVimのキーバインドを利用するためには、いくつかの設定を`.tmux.conf`ファイルに追加する必要があります。これにより、`hjkl`キーでカーソル移動ができるようになります。

```bash
# .tmux.confに追加
setw -g mode-keys vi
bind-key -T copy-mode-vi v send -X begin-selection
bind-key -T copy-mode-vi y send -X copy-selection
```

この設定を追加した後、TMUXを再起動するか、以下のコマンドを実行して設定をリロードしてください。

```bash
tmux source-file ~/.tmux.conf
```

## ステップ3: Visual Modeでのテキスト選択

TMUX内でテキストのコピーを始めるには、`Ctrl+b [` を押してコピーモードに入ります。次に、`hjkl`キーを使ってカーソルを移動し、コピーしたいテキストの開始位置にカーソルを合わせます。

コピーしたい箇所を選択開始するには `v` を押し、Vimのビジュアルモードのようにテキストを選択します。選択範囲は `hjkl` を使って調整できます。

## ステップ4: テキストのコピー

選択が完了したら、`y`を押してテキストをコピーします。これで、TMUXのバッファにテキストが保存されます。

## ステップ5: ペースト操作

TMUXの外でペーストを行うには、TMUXセッションを終了するか、新しいタブ/ウィンドウを開いて、通常通り`Command + v`（Macの場合）または`Ctrl + v`（Windows/Linuxの場合）を使ってペーストします。
