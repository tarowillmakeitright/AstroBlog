---
author: Taro Gray
pubDatetime: 2023-11-23T10:54:00.547Z
title: 【MySQL構文】INSERT INTO SET vs INSERT INTO VALUES の違い
postSlug: mysql-4
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - MySQL
  - INSERT INTO
  - INSERT INTO SET
description: "SQLにおける `DELETE` と `UPDATE` ステートメントは、データベース内のデータを変更するために使用されます。これらのコマンドはデータを操作する強力なツールであり、適切に使用することが重要です。"
---

## テーブルの構造

## INSERT INTO SET vs INSERT INTO VALUES の違い

SQLにおける `INSERT INTO` ステートメントは、データベースに新しい行を追加するための基本的な方法です。このステートメントには主に二つの書き方があります：`INSERT INTO SET` と `INSERT INTO VALUES`。

## INSERT INTO SET

`INSERT INTO SET` は、MySQLにおいて、各列に値を割り当てるより読みやすい方法です。この文法では、各列とその値を `SET` キーワードの後に列挙します。

### 例

```sql
INSERT INTO GalacticTravelers SET
  name = 'John Doe',
  occupation = 'Space Explorer',
  destination = 'Mars';
```

このクエリは、「GalacticTravelers」というテーブルに新しい行を追加し、各列に個別に値を設定します。

## INSERT INTO VALUES

`INSERT INTO VALUES` は、SQL標準の文法であり、列の値を括弧内にコンマ区切りで並べます。この方法は、どの値がどの列に対応するのかを正確に知っている必要があります。

### 例

```sql
INSERT INTO GalacticTravelers (name, occupation, destination)
VALUES ('Jane Smith', 'Astronomer', 'Venus');
```

このクエリは、`GalacticTravelers` テーブルの `name`, `occupation`, `destination` 列にそれぞれ値を挿入します。

## まとめ

`INSERT INTO SET` は、特に列が多いテーブルでのデータ挿入において、どの値がどの列に対応するのかを明確にするのに役立ちます。一方で `INSERT INTO VALUES` は、短く簡潔な書き方ができ、SQL標準に準拠しているため、多くのデータベースシステムで幅広くサポートされています。
