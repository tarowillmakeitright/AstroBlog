---
author: Taro Gray
pubDatetime: 2024-05-07T16:03:00.000Z
title: BashスクリプトにおけるCase文の活用
postSlug: linux-switch-statement
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
  - linux switch statement
description: Bash スクリプトでは、`case` 文を使用して複数の条件分岐を簡単に扱うことができます。この記事では、ファイル名のパターンマッチングとパイプラインを使用したデータ処理に焦点を当てて解説します。
---

## Table of contents

## `case` 文の基本

`case` 文は、ある変数や式の値に応じて異なるコマンドを実行するために使用します。構文は以下の通りです：

```bash
case "value" in
  pattern1)
    command1
    ;;
  pattern2)
    command2
    ;;
  *)
    default_command
    ;;
esac
```

## ファイル名のパターンマッチング

特に、ファイル拡張子に基づいて特定のアクションを実行する場合に便利です。例えば、すべてのテキストファイル（\*.txt）に対して何か操作をしたい場合は、以下のように記述します：

```bash
for filename in *.txt
do
  case "$filename" in
    *.txt)
      echo "Processing $filename"
      ;;
    *)
      echo "Ignoring $filename"
      ;;
  esac
done
```

このスクリプトは、ディレクトリ内のすべての `.txt` ファイルに対して処理を行います。

## パイプラインとの組み合わせ

パイプライン (`|`) を使用することで、あるコマンドの出力を別のコマンドへ直接渡すことができます。`case` 文と組み合わせることで、出力内容に応じた分岐処理を行うことも可能です。例えば：

```bash
echo "Please enter a filename: "
read filename
file "$filename" | case "$(cat)" in
  *"ASCII text"*)
    echo "$filename is a text file."
    ;;
  *)
    echo "$filename is not a text file."
    ;;
esac
```

この例では、`file` コマンドを使用してファイルタイプを確認し、その結果に基づいてテキストファイルかどうかを判定しています。

## まとめ

`case` 文は、Bash スクリプトで複雑な条件分岐を簡潔に記述するのに非常に有効です。特にファイル処理やコマンド出力の分岐には、パターンマッチングとパイプラインの組み合わせが強力なツールとなります。

この記事が皆さんのBashスクリプトの理解を深める助けとなれば幸いです。さらに学びたい方は、[GNU Bashマニュアル](https://www.gnu.org/software/bash/manual/bash.html)や他のオンラインリソースを参照してください。
