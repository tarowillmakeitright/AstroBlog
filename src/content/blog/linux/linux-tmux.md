---
author: Taro Gray
pubDatetime: 2024-04-14T12:13:00.000Z
title: tmuxの基本：ターミナルのプロになるためのガイド
postSlug: linux-tmux
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
  - tmux
description: tmuxは強力なターミナルマルチプレクサで、一つの画面で複数のターミナルセッションを管理することができます。このツールは、特にサーバーを管理したり、リモート作業を行う際に便利です。以下に、tmuxの基本的なコマンドと操作方法を紹介し、ブログ記事としてまとめます。
---

## Table of contents

tmuxは、1つの画面内で複数のターミナルセッションを扱える便利なツールです。ここではtmuxの基本的な使い方とよく使用されるコマンドについて解説します。

## tmuxのインストール

tmuxは多くのLinuxディストリビューションのパッケージリポジトリに含まれています。Ubuntuの場合、以下のコマンドでインストールできます。

```bash
sudo apt install tmux
```

## 基本的なコマンド

1. **新しいセッションの開始**:

   ```bash
   tmux
   ```

   これで新しいtmuxセッションが開始されます。

2. **セッションの一覧表示**:

   ```bash
   tmux ls
   ```

   現在アクティブなtmuxセッションの一覧を表示します。

3. **既存のセッションにアタッチ**:

   ```bash
   tmux attach -t セッション名
   ```

   特定のセッションに再接続します。

4. **セッションからデタッチ**:

   - `Control + b` と次に `d` を押します。
     これにより、セッションは背後で実行され続け、ユーザーは通常のターミナルに戻ります。

5. **tmuxのサーバーを終了**:

   ```bash
   tmux kill-server
   ```

   これにより、すべてのセッションが終了し、tmuxサーバーが停止します。

6. **現在の時刻を表示**:
   - `Control + b` と次に `t` を押します。
     ターミナル上に大きな時計が表示されます。

## その他の便利なコマンド

- **ウィンドウの作成**:

  - `Control + b` と次に `c` を押します。
    新しいウィンドウを開始します。

- **パネルの分割**:

  - 水平分割: `Control + b` と次に `"` を押します。
  - 垂直分割: `Control + b` と次に `%` を押します。

- **パネル間の移動**:
  - `Control + b` と矢印キーでパネル間を移動します。

## 参考ウェブサイト

- [tmux GitHub ページ](https://github.com/tmux/tmux) - tmuxの最新情報とドキュメントがあります。
- [tmuxチートシート](https://tmuxcheatsheet.com/) - よく使われるtmuxのコマンドがまとめられています。
- [tmuxの公式マニュアル](https://man7.org/linux/man-pages/man1/tmux.1.html) - より詳細な情報が記載されています。

tmuxを使用することで、ターミナルのセッション管理が非常に便利になり、特に複数の作業を同時に行う際の生産性が向上します。このガイドがあなたのUnix系OSで

の作業効率化に役立つことを願っています。
