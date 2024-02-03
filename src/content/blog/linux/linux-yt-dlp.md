---
author: Taro Gray
pubDatetime: 2024-02-03T13:20:00.000Z
title: 【Linuxコマンドマスターシリーズ】yt-dlp：究極のメディアダウンロードツール
postSlug: linux-yt-dlp
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
  - yt-dlp
description: `yt-dlp`は、その強力な機能と柔軟性で、オンラインビデオやオーディオのダウンロードにおいて最適なツールです。この記事で紹介した機能を活用して、あなたのメディアコンテンツのダウンロードをさらに便利にしましょう。
---

## Table of contents

## Unix環境でyt-dlpをマスターする

`yt-dlp`は、YouTubeやその他のビデオ共有サイトからメディアをダウンロードするための強力なコマンドラインツールです。このブログでは、Unix系システム（LinuxやmacOS）での`yt-dlp`の基本的な使い方から、中級者向けの高度な使用法までを紹介します。

## インストール方法

最新版の`yt-dlp`をインストールするには、以下のコマンドを実行します。

```bash
sudo curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
sudo chmod a+rx /usr/local/bin/yt-dlp
```

これにより、`yt-dlp`がダウンロードされ、実行可能な状態に設定されます。

## 基本的な使い方

指定されたURLのビデオをダウンロードする基本的なコマンドは次のとおりです。

```bash
yt-dlp https://www.youtube.com/watch?v=example
```

## 中級者向けの高度な使用法

### オーディオのみをダウンロード

ビデオからオーディオトラックのみを抽出してダウンロードします。

```bash
yt-dlp -x --audio-format mp3 https://www.youtube.com/watch?v=example
```

### 特定のフォーマットでダウンロード

利用可能なフォーマットを確認し、特定のフォーマットでダウンロードします。

```bash
yt-dlp -F https://www.youtube.com/watch?v=example
yt-dlp -f <フォーマットコード> https://www.youtube.com/watch?v=example
```

### プレイリストのダウンロード

YouTubeのプレイリスト全体をダウンロードします。

```bash
yt-dlp -i https://www.youtube.com/playlist?list=example
```

### 字幕のダウンロード

ビデオと共に字幕をダウンロードします。

```bash
yt-dlp --write-sub --sub-lang en https://www.youtube.com/watch?v=example
```

## yt-dlpのアップデート

`yt-dlp`がpip経由でインストールされている場合、以下のコマンドでアップデートします。

```bash
pip install --upgrade yt-dlp
```

特定のバージョンに更新したい場合は、アンインストール後に指定のバージョンをインストールします。

```bash
pip uninstall yt-dlp
pip install yt-dlp==2022.11.11
```

## 参考文献

- [yt-dlp GitHub ページ](https://github.com/yt-dlp/yt-dlp)
- [yt-dlp ドキュメント](https://github.com/yt-dlp/yt-dlp#readme)

`yt-dlp`は、その強力な機能と柔軟性で、オンラインビデオやオーディオのダウンロードにおいて最適なツールです。この記事で紹介した機能を活用して、あなたのメディアコンテンツのダウンロードをさらに便利にしましょう。
