---
author: Taro Gray
pubDatetime: 2024-02-03T12:23:00.000Z
title: 【Linuxコマンドマスターシリーズ】`yt-dlp`：究極のメディアダウンロードツール
postSlug: linux-yt-dlp
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
  - yt-dlp
description: Unix環境での`yt-dlp`の使用方法についてのブログ記事を、中級者向けのレベルでMarkdown形式で作成します。`yt-dlp`は、YouTubeやその他のビデオ共有サイトからメディアをダウンロードするためのコマンドラインプログラムです。ここでは、`yt-dlp`の基本的な使い方から、少し高度な使い方までを紹介し、コード例を交えて解説します。
---

## Table of contents

## `yt-dlp`：究極のメディアダウンロードツール

`yt-dlp`は、YouTubeをはじめとする数百のビデオ共有サイトからビデオやオーディオをダウンロードできる強力なツールです。この記事では、`yt-dlp`のインストール方法から、基本的な使用法、そしていくつかの高度な機能までをカバーします。

## `yt-dlp`のインストール

Unix系システム（LinuxやmacOS）で`yt-dlp`をインストールするには、以下のコマンドを使用します。

```bash
sudo curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o /usr/local/bin/yt-dlp
sudo chmod a+rx /usr/local/bin/yt-dlp
```

このコマンドは、最新版の`yt-dlp`をダウンロードし、実行可能な状態にします。

## 基本的な使い方

以下のコマンドは、指定されたURLのビデオをダウンロードします。

```bash
yt-dlp https://www.youtube.com/watch?v=example
```

## オーディオのみをダウンロード

ビデオからオーディオトラックのみを抽出してダウンロードするには、以下のコマンドを使用します。

```bash
yt-dlp -x --audio-format mp3 https://www.youtube.com/watch?v=example
```

## 特定のフォーマットを指定してダウンロード

利用可能なフォーマットのリストを表示し、特定のフォーマットでダウンロードするには、以下のコマンドを使用します。

```bash
yt-dlp -F https://www.youtube.com/watch?v=example
yt-dlp -f <フォーマットコード> https://www.youtube.com/watch?v=example
```

## プレイリストのダウンロード

YouTubeのプレイリスト全体をダウンロードするには、以下のコマンドを使用します。

```bash
yt-dlp -i https://www.youtube.com/playlist?list=example
```

`-i`オプションは、エラーが発生しても処理を続行します。

## 字幕のダウンロード

ビデオと共に字幕もダウンロードするには、以下のコマンドを使用します。

```bash
yt-dlp --write-sub --sub-lang en https://www.youtube.com/watch?v=example
```

## 参考文献とリンク

- `yt-dlp` GitHub ページ: [https://github.com/yt-dlp/yt-dlp](https://github.com/yt-dlp/yt-dlp)
- `yt-dlp` ドキュメント: [https://github.com/yt-dlp/yt-dlp#readme](https://github.com/yt-dlp/yt-dlp#readme)

`yt-dlp`は、その強力な機能と柔軟性で、オンラインのビデオやオーディオのダウンロードにおいて最適なツールです。この記事で紹介した機能を活用して、メディアコンテンツのダウンロードをさらに便利にしましょう。

## 正しいフォーマットの指定方法

`-f`オプションを使って、特定のフォーマットを指定する例は以下の通りです：

- **最高画質のビデオをダウンロード**:

  ```bash
  yt-dlp -f best [URL]
  ```

- **特定のフォーマット（例：mp4）でダウンロード**:

  ```bash
  yt-dlp -f mp4 [URL]
  ```

- **ビデオとオーディオを別々にダウンロードし、自動的に結合**:
  ```bash
  yt-dlp -f bestvideo+bestaudio [URL]
  ```

## フォーマットの一覧を取得

利用可能なフォーマットの一覧を表示するには、`-F`オプションを使用します：

```bash
yt-dlp -F [URL]
```

このコマンドは、指定したURLのメディアに対して利用可能なすべてのフォーマットを一覧表示します。その後、`-f`オプションを使用して、希望のフォーマットを指定できます。

## 注意点

`yt-dlp`コマンドのオプションや使用法については、公式のドキュメントや`yt-dlp --help`コマンドを参照してください。コマンドの構文やオプションはアップデートによって変更されることがあるため、最新の情報を確認することが重要です。

もし`-b`というオプションについて言及したい場合、それは恐らく誤解か、または別のコマンドやコンテキストに特有のオプションかもしれません。`yt-dlp`での使用においては、適切なフォーマット指定やその他のオプションの使用に焦点を当てることをお勧めします。

## `yt-dlp`を特定のバージョンにアップデートする方法

1. **現在の`yt-dlp`をアンインストール**:

   ```bash
   pip uninstall yt-dlp
   ```

2. **特定のバージョンを指定してインストール**:
   指定したバージョン`2022.11.11`にアップデート（再インストール）します。

   ```bash
   pip install yt-dlp==2022.11.11
   ```

   このコマンドは、`yt-dlp`を指定されたバージョンにインストールします。ただし、`2022.11.11`がPyPiで利用可能なバージョンである必要があります。利用可能なバージョンは[PyPiの`yt-dlp`ページ](https://pypi.org/project/yt-dlp/)で確認できます。

## `yt-dlp`を最新バージョンにアップデートする

特定のバージョンではなく、単に最新バージョンにアップデートしたい場合は、以下のコマンドを使用します。

```bash
pip install --upgrade yt-dlp
```

このコマンドは`yt-dlp`を最新バージョンにアップデートします。

## 注意

- `pip`コマンドを使用する際は、Pythonの環境（システムのPython、ユーザーのPython、仮想環境など）を意識することが重要です。適切な環境でコマンドを実行しているか確認してください。
- 特定のバージョンが必要な理由（依存性の問題、新機能のテスト、バグの回避など）に応じて、インストールするバージョンを選択してください。

`yt-dlp`のような活発に開発されているプロジェクトでは、頻繁に新機能が追加されたり、バグが修正されたりするため、可能であれば定期的に最新バージョンに更新することをお勧めします。
