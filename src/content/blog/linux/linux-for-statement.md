---
author: Taro Gray
pubDatetime: 2024-05-07T15:41:00.000Z
title: BashスクリプトにおけるForループの活用
postSlug: linux-for-statement
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
  - linux for statement
description: Bash スクリプトでは、`for` ループは反復処理を行う際に非常に重要な役割を果たします。この記事では、`$@`, `seq`, および `in` キーワードを使った `for` ループの具体的な使い方を紹介します。
---

## Table of contents

Bash スクリプトでは、`for` ループは反復処理を行う際に非常に重要な役割を果たします。この記事では、`$@`, `seq`, および `in` キーワードを使った `for` ループの具体的な使い方を紹介します。

## `$@` を使ったループ

`$@` は、スクリプトに渡されたすべての位置パラメータを含む特殊変数です。スクリプトに複数の引数が渡された場合、`$@` を使ってそれらを順に処理することができます。

```bash
#!/bin/bash
# すべての引数に対して何かの操作を行うスクリプト
for arg in "$@"
do
  echo "引数: $arg"
done
```

このスクリプトは、渡された各引数を画面に表示します。

## `seq` を使用した数値のループ

`seq` コマンドは、指定された数値のシーケンスを生成します。これを `for` ループと組み合わせて、特定の範囲の数値に対して操作を行うことができます。

```bash
#!/bin/bash
# 1から10までの数を出力
for num in $(seq 1 10)
do
  echo "数値: $num"
done
```

この例では、1から10までの数値が順に出力されます。

## `in` キーワードの使用

`in` キーワードは、`for` ループで処理する要素を指定するのに使用します。リスト内の各要素に対してループを実行します。

```bash
#!/bin/bash
# 特定の文字列に対して操作を行う
for item in "apple" "banana" "cherry"
do
  echo "フルーツ: $item"
done
```

このスクリプトは、リスト内の各フルーツ名を順に出力します。

## まとめ

Bash スクリプトの `for` ループは、複数のデータや引数に対して同じ操作を繰り返し実行する際に非常に便利です。`$@`, `seq`, および `in` キーワードを理解し、適切に利用することで、スクリプトの柔軟性と効率を高めることができます。

この記事が皆さんのBashスクリプトの理解を深める助けとなれば幸いです。もっと学びたい方は、[GNU Bashマニュアル](https://www.gnu.org/software/bash/manual/bash.html)や[Linux Command Line](https://www.linuxcommand.org/)などの資源を参考にしてください。
