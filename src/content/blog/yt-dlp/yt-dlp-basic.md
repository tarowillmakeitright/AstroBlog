---
author: Taro Gray
pubDatetime: 2024-05-26T12:58:00.000Z
title:
postSlug: yt-dlp-basic
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - yt-dlp
description: YouTube動画をMP3としてダウンロードする方法
---

## Table of contents

## YouTube動画をMP3としてダウンロードする方法

## YouTube動画をMP3としてダウンロード

コマンドラインで以下のコマンドを入力します。URLはダウンロードしたい動画のURLに置き換えてください。

```sh
yt-dlp -x --audio-format mp3 "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
```

## YouTube動画を（音声+映像）ダウンロード

動画をそのまま（映像と音声付きで）ダウンロードしたい場合は、以下のように`yt-dlp`とYouTube動画のURLを使います。

```sh
yt-dlp "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
```

## 複数のYouTube動画を（フル音声+映像）ダウンロード

上記のコマンドを複数回使用することもできますが、もっと簡単な方法があります。

まず、YouTubeでダウンロードしたい動画をプレイリストに追加します。プレイリストを作成し、そこに動画を追加してください。プレイリストのURLを取得します。URLは次のような形式になります。

```
https://www.youtube.com/playlist?list=PLlaN88a7y2_rosKX2WQt2VjFbjyDQXOkR
```

このURLを使用して以下のように`yt-dlp`コマンドを実行します。

```sh
yt-dlp -i "https://www.youtube.com/playlist?list=PLlaN88a7y2_rosKX2WQt2VjFbjyDQXOkR"
```

注意: プレイリストは公開（PUBLIC）または限定公開（UNLISTED）でなければなりません。プレイリストが非公開（PRIVATE）の場合はダウンロードできません。ただし、ログイン済みのYouTubeアカウントからアクセスできる場合に限り、ブラウザのクッキーを使用して非公開動画をダウンロードする新しいオプションがあります。

```sh
yt-dlp --cookies-from-browser chrome "<YOUTUBE URL>"
```

## 複数のYouTube動画をMP3としてダウンロード

プレイリストの動画をMP3としてダウンロードする場合も同様です。以下のコマンドを使用し、リストIDを自分のリストIDに置き換えます。

```sh
yt-dlp -x --audio-format mp3 -i PLlaN88a7y2_rosKX2WQt2VjFbjyDQXOkR
```

## 動画の画質を選択

動画の画質を選択する方法を提供してくれたu/x1996xに感謝します。彼は、古い`youtube-dl`コマンドが`yt-dlp`で機能しない問題に直面していました。例を見て試したところ、次のコマンドが機能することが分かりました。

```sh
yt-dlp -f "bv*[height<=1080][ext=mp4]+ba[ext=m4a]/b[height<=1080][ext=mp4] / bv*+ba/b"
```

詳細な解説は彼のコメントを参照してください。素晴らしい内容です。ありがとう、u/x1996x!

---

## ブログ形式 (Markdown)

```md
# YouTube動画をMP3としてダウンロードする方法

## YouTube動画をMP3としてダウンロード

コマンドラインで以下のコマンドを入力します。URLはダウンロードしたい動画のURLに置き換えてください。
```

yt-dlp -x --audio-format mp3 "https://www.youtube.com/watch?v=dQw4w9WgXcQ"

```

## YouTube動画を（音声+映像）ダウンロード
動画をそのまま（映像と音声付きで）ダウンロードしたい場合は、以下のように`yt-dlp`とYouTube動画のURLを使います。

```

yt-dlp "https://www.youtube.com/watch?v=dQw4w9WgXcQ"

```

## 複数のYouTube動画を（フル音声+映像）ダウンロード
上記のコマンドを複数回使用することもできますが、もっと簡単な方法があります。

まず、YouTubeでダウンロードしたい動画をプレイリストに追加します。プレイリストを作成し、そこに動画を追加してください。プレイリストのURLを取得します。URLは次のような形式になります。

```

https://www.youtube.com/playlist?list=PLlaN88a7y2_rosKX2WQt2VjFbjyDQXOkR

```

このURLを使用して以下のように`yt-dlp`コマンドを実行します。

```

yt-dlp -i "https://www.youtube.com/playlist?list=PLlaN88a7y2_rosKX2WQt2VjFbjyDQXOkR"

```

注意: プレイリストは公開（PUBLIC）または限定公開（UNLISTED）でなければなりません。プレイリストが非公開（PRIVATE）の場合はダウンロードできません。ただし、ログイン済みのYouTubeアカウントからアクセスできる場合に限り、ブラウザのクッキーを使用して非公開動画をダウンロードする新しいオプションがあります。

```

yt-dlp --cookies-from-browser chrome "<YOUTUBE URL>"

```

## 複数のYouTube動画をMP3としてダウンロード
プレイリストの動画をMP3としてダウンロードする場合も同様です。以下のコマンドを使用し、リストIDを自分のリストIDに置き換えます。

```

yt-dlp -x --audio-format mp3 -i PLlaN88a7y2_rosKX2WQt2VjFbjyDQXOkR

```

## 動画の画質を選択
動画の画質を選択する方法を提供してくれたu/x1996xに感謝します。彼は、古い`youtube-dl`コマンドが`yt-dlp`で機能しない問題に直面していました。例を見て試したところ、次のコマンドが機能することが分かりました。

```

yt-dlp -f "bv*[height<=1080][ext=mp4]+ba[ext=m4a]/b[height<=1080][ext=mp4] / bv*+ba/b"

```

```
