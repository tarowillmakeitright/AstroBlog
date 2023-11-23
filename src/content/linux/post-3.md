---
author: Taro Gray
pubDatetime: 2023-11-23T110:43:00.000Z
title: 【Linuxコマンドマスターシリーズ】ペーストと検索の秘密
postSlug: post-3
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
  - Linuxコマンド
  - Ctrl + y
  - Ctrl + r
description: "第3回のブログ記事をMarkdown形式で作成します。今回はペーストと検索に関するコマンドを面白く、実用的に紹介します。タイトルは「Linuxコマンドマスターシリーズ：ペーストと検索の秘密」にしましょう。"
---

## Table of contents

## Linuxコマンドマスターシリーズ：ペーストと検索の秘密

皆さん、こんにちは！Linuxの魔法学校へ再びようこそ。今回は、ペーストと検索の魔法に焦点を当てます。これらの魔法を使いこなせば、あなたのターミナル操作はまるで魔術師のようにスムーズになるでしょう！

## Ctrl + y：ペーストの魔法

「Ctrl + k」や「Ctrl + w」でカットしたテキストを思い出す方法は？正解は「Ctrl + y」です！これで、カットしたテキストをペーストできます。まるでタイムカプセルを開けるような感覚です。

```bash
# "sudo apt-get update"と打った後...
sudo apt-get update
# Ctrl + uを使って全てカット
[]
# Ctrl + yでペーストして復活！
sudo apt-get update
```

## Ctrl + r：履歴の探偵

過去に実行したコマンドを探すのは、まるで探偵のよう。でも「Ctrl + r」を使えば、コマンド履歴の探偵になれます。打ち始めると、履歴から合致するコマンドを見つけ出してくれます。

```bash
# Ctrl + rを押して検索開始
(reverse-i-search)`':
# "upd"とタイプすると...
(reverse-i-search)`upd': sudo apt-get update
```

## まとめ：ペーストと検索の達人

今回学んだ「Ctrl + y」と「Ctrl + r」の魔法で、あなたのLinux操作はもっと効率的に、そして楽しくなるでしょう。次回は、さらに高度なコマンドのテクニックを紹介します。お楽しみに！
