---
author: Taro Gray
pubDatetime: 2023-11-23T10:50:00.547Z
pubDatetime: 2023-11-23T10:50:00.547Z
title: 【MySQL構文】DELETE文とUPDATE文の基本
postSlug: mysql-2
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - MySQL
  - DELETE
  - UPDATE
description: "SQLにおける `DELETE` と `UPDATE` ステートメントは、データベース内のデータを変更するために使用されます。これらのコマンドはデータを操作する強力なツールであり、適切に使用することが重要です。"
---

## Table of contents

## DELETE文とUPDATE文の基本

SQLにおける `DELETE` と `UPDATE` ステートメントは、データベース内のデータを変更するために使用されます。これらのコマンドはデータを操作する強力なツールであり、適切に使用することが重要です。

## DELETE文

`DELETE` 文は、データベースから行を削除するために使用されます。このコマンドを使用するときは、特定の条件を指定して、どの行を削除するかを明確にする必要があります。

### 例

想像してみてください：「PlanetaryVisits」というテーブルがあり、これにはさまざまな惑星への訪問記録が含まれています。`DELETE` 文を使用して、特定の惑星への訪問記録を削除することができます。

```sql
DELETE FROM PlanetaryVisits
WHERE planet = 'Pluto';
```

このクエリは、「Pluto」という惑星へのすべての訪問記録を `PlanetaryVisits` テーブルから削除します。

## UPDATE文

`UPDATE` 文は、既存のデータベース内の行のデータを変更するために使用されます。`SET` キーワードを使用して、特定の列の新しい値を指定します。

### 例

`GalacticTravelers` テーブルがあり、隊員の職業を更新する必要があるとしましょう。

```sql
UPDATE GalacticTravelers
SET occupation = 'Interstellar Ambassador'
WHERE name = 'John Doe';
```

このクエリは、`GalacticTravelers` テーブルで `name` が 'John Doe' の隊員の職業を 'Interstellar Ambassador' に更新します。

## まとめ

`DELETE` と `UPDATE` ステートメントは、データベース内のデータを管理するために非常に強力です。これらのコマンドを使用する際は、特に `WHERE` 句を適切に使用して、意図した行だけが影響を受けるように注意する必要があります。面白くて想像力豊かな宇宙の例を通じて、これらのSQLコマンドの基本的な使用法と重要性を理解することができます。
