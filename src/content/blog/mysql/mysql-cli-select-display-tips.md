---
author: Taro Gray
pubDatetime: 2024-08-24T14:57:00.00Z
title: MySQL CLIで見やすいデータ表示方法
postSlug: mysql-cli-select-display-tips
featured: true
draft: false
ogImage: https://example.com/path-to-your-ogimage.png
tags:
  - MySQL
  - CLI
  - データベース
  - 開発環境
description: MySQL CLIで`SELECT * FROM table`を実行した際にデータが見づらい場合の対処法を紹介します。見やすくするための様々な方法を解説します。
---

## 目次

## はじめに

MySQLのCLIで`SELECT * FROM table`を実行すると、出力結果が見づらいことがあります。本記事では、データを見やすく表示するためのさまざまな方法を紹介します。

## データ表示を見やすくする方法

### \Gを使った縦表示

クエリの末尾に`\G`を付けると、結果を縦に表示できます。各列が個別の行として表示されるため、データが多い場合でも視認性が向上します。

```sql
SELECT * FROM table_name\G
```

### 必要な列のみを表示

`SELECT *`を使う代わりに、必要な列を指定することで、データの量を減らして見やすくすることができます。

```sql
SELECT column1, column2 FROM table_name;
```

### lessコマンドを使ってページング

結果が多い場合、`less`コマンドを使ってページング表示することができます。特にUnix系システムで便利です。

```sh
mysql -u username -p -e "SELECT * FROM table_name" | less -S
```

`less -S`オプションを使うことで、横スクロールも可能になります。

### データをファイルに出力して確認

大量のデータを扱う場合、結果をファイルに出力してテキストエディタで確認するのも一つの方法です。

```sh
mysql -u username -p -e "SELECT * FROM table_name" > output.txt
```

### 列の幅を調整

デフォルトの列幅が広すぎて見づらい場合は、自動的に縦表示に切り替わるオプションを使用することができます。

```sh
mysql -u username -p --auto-vertical-output -e "SELECT * FROM table_name"
```

## まとめ

MySQL CLIでのデータ表示を改善するための方法を紹介しました。これらのテクニックを活用することで、クエリ結果を効率よく確認できるようになります。日々の作業に取り入れて、データベース操作をスムーズに進めましょう。
