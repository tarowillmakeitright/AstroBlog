---
author: Taro Gray
pubDatetime: 2023-12-24T02:17:00.547Z
title: 【MySQL構文】INSERT INTO SET vs INSERT INTO VALUES の違い
postSlug: mysql-insert-into-select
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - MySQL
  - INSERT INTO SELECT
description: MySQLの世界では、データを一箇所から別の箇所に瞬時に転送する魔法があります。その魔法の名前は`INSERT INTO ... SELECT`です。このコマンドは、データベースのテーブルから直接データを読み込み、別のテーブルに効率的に挿入するために使用されます。今回は、この魔法の使い方と、それを使ったちょっとした冒険話を紹介しましょう。
---

## Table of contents

## 魔法のようなMySQLコマンド：`INSERT INTO ... SELECT`

MySQLの世界では、データを一箇所から別の箇所に瞬時に転送する魔法があります。その魔法の名前は`INSERT INTO ... SELECT`です。このコマンドは、データベースのテーブルから直接データを読み込み、別のテーブルに効率的に挿入するために使用されます。今回は、この魔法の使い方と、それを使ったちょっとした冒険話を紹介しましょう。

## 基本的な呪文：`INSERT INTO ... SELECT` の使い方

```sql
INSERT INTO target_table (column1, column2, ...)
SELECT column1, column2, ...
FROM source_table
WHERE condition;
```

この呪文では、`source_table`のデータを`target_table`に挿入します。条件（`WHERE`節）を使って、特定のデータのみを選択することができます。

## 面白い例：ハッカー対策

想像してみてください。ある日、あなたのデータベースにハッカーが侵入しました。しかし、あなたは賢明にも重要なデータを一時的なテーブルに移動させており、ハッカーは何も盗めませんでした。

```sql
INSERT INTO temporary_safehouse (id, secret_data)
SELECT id, secret_data
FROM main_vault
WHERE alert_level = 'RED';
```

このクエリでは、`main_vault`から`temporary_safehouse`へと、警戒レベルが「赤」のすべての秘密データが緊急避難されます。

## ハッカーの逆襲

しかし、ハッカーは諦めません。彼らは偽のデータを`main_vault`に挿入しようと計画しました。でも、あなたは一枚上手でした。

```sql
INSERT INTO main_vault (id, secret_data)
SELECT id, fake_data
FROM hacker_traps
WHERE detected_hacker = 'YES';
```

このクエリでは、ハッカーが仕掛けた罠（`hacker_traps`テーブル）を利用して、偽のデータで`main_vault`を埋め尽くします。ハッカーは混乱し、撤退しました。

## 結論

`INSERT INTO ... SELECT`は、データを効率的に移動させたり、特定の条件に基づいてデータを挿入したりするのに非常に便利です。このコマンドを使いこなせば、データベースの魔法使いとして、あらゆる状況に対応できるでしょう。ただし、大量のデータを扱う場合はパフォーマンスへの影響に注意してください。ハッカーのような予期せぬ訪問者にも備え、データの安全を常に最優先しましょう。
この記事は、`INSERT INTO ... SELECT`の基本的な使用法と、それを使ったユニークなシナリオを紹介することで、読者に楽しく学んでもらうことを目指しています。ハッカーとの架空の戦いを通じて、このコマンドの潜在的な使い方を探求します。
