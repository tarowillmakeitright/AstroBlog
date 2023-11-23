---
author: Taro Gray
pubDatetime: 2023-11-23T10:56:00.00Z
title: 【MySQL構文】SQLのLIKE構文の使い方
postSlug: post-6
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - MySQL
  - LIKE
description: SQLの `LIKE` 構文は、文字列の検索に使用される強力なツールです。特に、あいまい検索やパターンマッチングに役立ちます。
---

## テーブルの構造

## SQLのLIKE構文の使い方

SQLの `LIKE` 構文は、文字列の検索に使用される強力なツールです。特に、あいまい検索やパターンマッチングに役立ちます。

## LIKE構文の基本

`LIKE` 構文では、2つのワイルドカード（`%` と `_`）が使用されます。

- `%` は任意の文字列を表します。
- `_` は任意の単一文字を表します。

## 面白いデータを用いた例

想像してみてください：「銀河系食品データベース」があり、様々な惑星の食品に関する情報が格納されています。このデータベースには、食品名、原材料、起源の惑星などの情報が含まれています。

- **データベーステーブル**:
  | FoodID | Name | Ingredient | OriginPlanet |
  |--------|----------------|---------------|--------------|
  | 1 | MarsBar | Chocolate | Mars |
  | 2 | VenusPie | Berries | Venus |
  | 3 | JupiterJelly | SpaceJelly | Jupiter |

### LIKE構文の使用例

1. **特定のパターンを含む名前を検索**:

   - 「Mars」で始まる食品名を検索する場合：
     ```sql
     SELECT * FROM GalacticFoods
     WHERE Name LIKE 'Mars%';
     ```
   - このクエリは、名前が「Mars」で始まるすべての食品を検索します（例：MarsBar）。

2. **特定の位置にある文字を検索**:
   - 名前の3文字目が「p」である食品を検索する場合：
     ```sql
     SELECT * FROM GalacticFoods
     WHERE Name LIKE '__p%';
     ```
   - このクエリは、名前の3文字目が「p」であるすべての食品を検索します（例：JupiterJelly）。

## まとめ

LIKE構文は、特定のパターンに基づいてデータベース内のデータを柔軟に検索するのに非常に便利です。銀河系食品データベースの例を通じて、LIKE構文の使い方とその有効性を楽しく理解できます。このツールを使用することで、膨大なデータベースから必要な情報を迅速かつ簡単に見つけることができます。
