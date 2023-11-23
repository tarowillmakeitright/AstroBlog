---
author: Taro Gray
pubDatetime: 2023-11-19T08:40:00.00Z
title: 【MySQL正規形】第一正規形（1NF）につついて学ぼう
postSlug: post-13
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - MySQL
  - 第1正規形
  - 1NF
  - 正規形
description: リレーショナルデータベース設計において、第一正規形（1NF）は基本的な正規化のステップです。1NFにすることで、データベース内のデータが整理され、より効率的に管理できるようになります。
---

## Table of contents

## 第一正規形（1NF）についての説明

リレーショナルデータベース設計において、第一正規形（1NF）は基本的な正規化のステップです。1NFにすることで、データベース内のデータが整理され、より効率的に管理できるようになります。

## 第一正規形とは？

1NFは、テーブル内の各フィールドが「原子的（分割不可能）」であることを要求します。つまり、各フィールドには重複やグループ化されたデータが含まれていてはならず、一つのデータ項目のみを含むべきです。

## 面白いデータを用いた例

想像してみてください：「宇宙船のクルー名簿」を管理するデータベースがあります。この名簿には、クルーメンバーの名前、役職、所属する惑星、お気に入りの宇宙食が記載されています。

- **非正規形のテーブル**:
  | CrewID | Name | Role | Planet | Favorite Foods |
  |--------|---------------|---------------|---------------|-----------------------|
  | 1 | John Doe | Captain | Earth | Pizza, Ice Cream |
  | 2 | Jane Smith | Science Officer | Mars | Sushi, Chocolate |
  | 3 | Mike Johnson | Engineer | Venus | Hamburger, Salad |

このテーブルは1NFを満たしていません。なぜなら、`Favorite Foods` フィールドが複数の項目（例：`Pizza, Ice Cream`）を含んでいるからです。

- **第一正規形のテーブル**:
  | CrewID | Name | Role | Planet | Favorite Food |
  |--------|---------------|-----------------|---------------|----------------|
  | 1 | John Doe | Captain | Earth | Pizza |
  | 1 | John Doe | Captain | Earth | Ice Cream |
  | 2 | Jane Smith | Science Officer | Mars | Sushi |
  | 2 | Jane Smith | Science Officer | Mars | Chocolate |
  | 3 | Mike Johnson | Engineer | Venus | Hamburger |
  | 3 | Mike Johnson | Engineer | Venus | Salad |

第一正規形に変換すると、`Favorite Foods` フィールドは原子的になり、各行が一つの食品を表します。これにより、データはより整理され、クエリが容易になります。

## まとめ

第一正規形は、データベース設計の最初のステップとして非常に重要です。宇宙船のクルー名簿のように、データを適切に整理することで、情報の取得と管理が効率的になります。面白い例を使うことで、1NFの概念をより楽しく、わかりやすく伝えることができます。
