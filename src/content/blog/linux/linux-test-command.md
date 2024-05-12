---
author: Taro Gray
pubDatetime: 2024-05-07T15:16:00.000Z
title: Linuxのテストコマンドと条件式の使い方
postSlug: linux-test-command
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
  - linux test
  - linux if
description: Linux では、ファイルやディレクトリに関する多くのテストが `test` コマンドや `[` コマンドを使用して行われます。これらのコマンドを使って、スクリプト内で条件分岐を行うことができます。
---

## Table of contents

## 主なテストオペレーター

以下に主なテストオペレーターを説明します。

- **`-e`**: ファイルが存在するかどうかをチェックします。
- **`-d`**: ファイルがディレクトリであるかをチェックします。
- **`-h`, `-L`**: ファイルがシンボリックリンクであるかをチェックします。
- **`-f`**: ファイルが通常のファイルであるかをチェックします。
- **`-r`**: ファイルが読み取り可能かをチェックします。
- **`-w`**: ファイルが書き込み可能かをチェックします。
- **`-x`**: ファイルが実行可能かをチェックします。
- **`file1 -nt file2`**: file1がfile2より新しい（最終変更時刻が後）かをチェックします。
- **`file1 -ot file2`**: file1がfile2より古い（最終変更時刻が前）かをチェックします。

## 論理演算子の使用

複数の条件を組み合わせるためには、以下の論理演算子を使用します。

- **`-a`**: AND 演算子（両方の条件が真の場合に真）
- **`-o`**: OR 演算子（少なくとも一つの条件が真の場合に真）
- **`!`**: NOT 演算子（条件の真偽を逆にする）
- **`( )`**: 条件をグループ化する

## 実用例

以下に、論理演算子を使った実用例を示します。

```bash
if [ -f "$FILE" -a -w "$FILE" ]; then
  echo "$FILE exists and is writable."
fi

if [ -f "$FILE" -o -d "$DIRECTORY" ]; then
  echo "Either $FILE is a file or $DIRECTORY is a directory."
fi

if [ ! -x "$FILE" ]; then
  echo "$FILE is not executable."
fi
```

これらの例は、複数のテスト条件を組み合わせてより複雑なロジックを実装する方法を示しています。

## 参考リンク

以下のリンクから、Linuxのテストコマンドに関するさらに詳しい情報を得ることができます。

- [GNU Coreutils - Test expressions](https://www.gnu.org/software/coreutils/manual/html_node/Test-expressions.html)
- [Linuxize - Using the Test Command in Linux](https://linuxize.com/post/how-to-compare-strings-in-bash/)
