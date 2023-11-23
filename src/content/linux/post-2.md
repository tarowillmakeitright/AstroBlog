---
author: Taro Gray
pubDatetime: 2023-11-23T10:45:00.000Z
title: 【Linuxコマンドマスターシリーズ】ハッカー風高度操作術
postSlug: post-2
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
  - Linuxコマンド
  - Ctrl + s
  - Ctrl + q
  - Ctrl + l
  - Ctrl + g
description: "こんにちは、Linuxの魔法使いの皆さん！今日は、ターミナルでの高度な操作を学び、ちょっとしたハッカー気分を味わいます。さあ、キーボードを手に取り、ターミナルの世界に潜入しましょう！"
---

## Table of contents

## Linuxコマンドマスターシリーズ：ハッカー風高度操作術

こんにちは、Linuxの魔法使いの皆さん！今日は、ターミナルでの高度な操作を学び、ちょっとしたハッカー気分を味わいます。さあ、キーボードを手に取り、ターミナルの世界に潜入しましょう！

## Ctrl + r → Enter → Esc → Ctrl + g：履歴の忍者

「Ctrl + r」でコマンド履歴を検索した後、見つけたコマンドを実行するのではなく、さらに編集したい場合はどうすればいいでしょう？Enterを押してからすぐにEscを押すと、コマンドを実行せずに編集モードに入ります。そして、やっぱりやめたいときは「Ctrl + g」でキャンセル。これであなたも履歴の忍者です！

```bash
# Ctrl + rで "sudo apt-get update" を検索
(reverse-i-search)`': sudo apt-get update
# Enter → Escを素早く押して編集モードに
sudo apt-get update
# もしやめたいなら、Ctrl + gでキャンセル
```

## ハッカー風の小技：ターミナルで遊ぶ

ターミナルでハッカー気分を味わいたい？ `cmatrix` というコマンドで、映画「マトリックス」のようなスクリーンセーバーを楽しむことができます。まるで、デジタル世界の中を飛び回るハッカーのよう！

```bash
# cmatrixをインストール（まだなら）
sudo apt-get install cmatrix

# cmatrixを実行して、マトリックス世界へ
cmatrix
```

## まとめ：ハッカー風の魔法使い

これで、あなたもLinuxターミナルのハッカー風魔法使いです。今回学んだ高度なコマンド操作や小技で、ターミナル操作がもっと楽しく、カッコよくなるはずです。次回も、さらに面白くて役立つLinuxの魔法を紹介します。お楽しみに！
