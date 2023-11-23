---
author: Taro Gray
pubDatetime: 2023-11-16T11:15:00.547Z
title: 【MySQL構文】INNER JOINについて学ぼう
postSlug: INNER JOINについて学ぼう
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - MySQL
  - INNER JOIN
description: "面白いデータを使って `INNER JOIN` の例を説明しましょう。想像してみてください：私たちには2つのテーブルがあります。「Wizards」（魔法使い）と「Spells」（呪文）。魔法使いはそれぞれ特定の呪文を使えるとしましょう。"
---

## Table of contents

面白いデータを使って `INNER JOIN` の例を説明しましょう。想像してみてください：私たちには2つのテーブルがあります。「Wizards」（魔法使い）と「Spells」（呪文）。魔法使いはそれぞれ特定の呪文を使えるとしましょう。

## テーブルの構造

1. **Wizards（魔法使い）**:

   - `wizard_id`：魔法使いのID。
   - `name`：魔法使いの名前。
   - `age`：魔法使いの年齢。

2. **Spells（呪文）**:
   - `spell_id`：呪文のID。
   - `name`：呪文の名前。
   - `effect`：呪文の効果。
   - `wizard_id`：この呪文を使える魔法使いのID。

## データ例

- **Wizards**:
  | wizard_id | name | age |
  |-----------|--------------|-----|
  | 1 | Gandalf | 201 |
  | 2 | Merlin | 175 |
  | 3 | Harry Potter | 17 |

- **Spells**:
  | spell_id | name | effect | wizard_id |
  |----------|-----------------|--------------------|-----------|
  | 1 | Levitation | 浮遊する | 1 |
  | 2 | Invisibility | 透明になる | 2 |
  | 3 | Lightning Bolt | 稲妻を放つ | 1 |
  | 4 | Teleportation | テレポートする | 3 |
  | 5 | Healing | 癒す | 2 |

## INNER JOINのクエリ

ここで、各魔法使いが使える呪文のリストを取得したいとします。これは `INNER JOIN` を使って実現できます：

```sql
SELECT Wizards.name, Spells.name, Spells.effect
FROM Wizards
INNER JOIN Spells ON Wizards.wizard_id = Spells.wizard_id;
```

## 結果

このクエリは、`Wizards` テーブルと `Spells` テーブルを `wizard_id` で結合し、魔法使いの名前と彼らが使える呪文の名前と効果をリストします。出力は以下のようになります：

| Wizard Name  | Spell Name     | Effect         |
| ------------ | -------------- | -------------- |
| Gandalf      | Levitation     | 浮遊する       |
| Gandalf      | Lightning Bolt | 稲妻を放つ     |
| Merlin       | Invisibility   | 透明になる     |
| Merlin       | Healing        | 癒す           |
| Harry Potter | Teleportation  | テレポートする |

## 解説

`INNER JOIN` は、2つのテーブル間の共通のデータを結合するのに使います。この例では、`Wizards` テーブルの `wizard_id` が `Spells` テーブルの `wizard_id` と一致する行を結合しています。これにより、各魔法使いと彼らが使える呪文の関係が明らかになります。

面白いデータを使うことで、`INNER JOIN` の動作を視覚的により理解しやすくなります。魔法使いと呪文の例は、データベースの概念を楽しく学ぶのに役立つでしょう。
