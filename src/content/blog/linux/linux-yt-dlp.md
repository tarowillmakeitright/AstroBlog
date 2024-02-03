---
author: Taro Gray
pubDatetime: 2024-02-03T21:15:00.000Z
title: Unixでの`yt-dlp`活用ガイド
postSlug: linux-yt-dlp
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
description: yt-dlpは高機能で柔軟なダウンロードツールです。このガイドを参考にして、Unix環境で`yt-dlp`を最大限に活用しましょう。
---

## Table of contents

`yt-dlp`は、YouTubeやその他のビデオ共有サイトからメディアをダウンロードするためのコマンドラインツールです。この記事では、`yt-dlp`のインストールから基本的な使用法、さらには特定のバージョンへのアップデート方法までをカバーします。

## インストール方法

Unix系システムで`yt-dlp`をインストールするには、以下のコマンドを実行します。

```bash
sudo curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
sudo chmod a+rx /usr/local/bin/yt-dlp
```

## 基本的な使用法

## ビデオのダウンロード

```bash
yt-dlp [ビデオURL]
```

## オーディオのみをダウンロード

```bash
yt-dlp -x --audio-format mp3 [ビデオURL]
```

## プレイリストのダウンロード

```bash
yt-dlp -i [プレイリストURL]
```

## 特定バージョンへのアップデート

`yt-dlp`がpipやPyPiでインストールされている場合、`pip`コマンドを使用してアップデートする必要があります。

## アップデート方法

```bash
pip install --upgrade yt-dlp
```

特定のバージョンにアップデートするには：

```bash
pip install yt-dlp==[バージョン番号]
```

## 注意点と参考リンク

- `yt-dlp`の使用法については、公式のドキュメントやGitHubページを参照してください。
- 特定のバージョンへのアップデートは、PyPiで利用可能なバージョンに限られます。

参考文献:

- [yt-dlp GitHub ページ](https://github.com/yt-dlp/yt-dlp)
- [yt-dlp ドキュメント](https://github.com/yt-dlp/yt-dlp#readme)
