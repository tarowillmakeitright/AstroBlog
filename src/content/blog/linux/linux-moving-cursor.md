---
author: Taro Gray
pubDatetime: 2023-11-23T10:42:00.00Z
title: 【Linuxコマンドマスターシリーズ】移動とナビゲーションの魔法
postSlug: linux-moving-cursor
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
description: こんにちは、Linuxの世界へようこそ！今日は、あなたがターミナルの魔法使いになるための最初の一歩を踏み出します。カーソル移動の基本から始めましょう。これらのコマンドは、まるで魔法のようにあなたのタイピング速度を上げるでしょう！
---

## Table of contents

## Linuxコマンドマスターシリーズ：移動とナビゲーションの魔法

こんにちは、Linuxの世界へようこそ！今日は、あなたがターミナルの魔法使いになるための最初の一歩を踏み出します。カーソル移動の基本から始めましょう。これらのコマンドは、まるで魔法のようにあなたのタイピング速度を上げるでしょう！

## Ctrl + b と Ctrl + f：時間を巻き戻す（と少し進める）

あなたが長いコマンドを入力していて、突然「あ、一文字間違えた！」と気づいたとき、どうしますか？マウスでクリック？いいえ、`Ctrl + b`で一文字戻り、`Ctrl + f`で一文字進むのです。これでタイムトラベルが可能に！

```bash
# 例: "gir clone"をタイプしてしまった...
gir clone
# Ctrl + bを2回押して、"i"に戻る
gi[r] clone
# "i"を削除して、"t"を追加
git clone
```

## Ctrl + a と Ctrl + e：文学的な旅路

あなたのカーソルが長いコマンドラインの文学的な旅をしているとき、`Ctrl + a`でその旅の始まり（行の先頭）へ、`Ctrl + e`で結末（行の末尾）へ瞬時にジャンプできます。まるで、本の中でページをパラパラめくるように。

```bash
# 長いコマンドを入力した後...
 sudo apt-get update
# Ctrl + aを押して、行の先頭へ
 [s]udo apt-get update
# Ctrl + eを押して、行の末尾へ
 sudo apt-get update[]
```

## まとめ：カーソルの魔法使い

これらのショートカットキーを覚えて、あなたもカーソルの魔法使いになりましょう。これで、あなたのLinuxコマンドラインは、以前よりもずっと素早く、効率的になるはずです。次回は、削除と編集の魔法について学びます。お楽しみに！
