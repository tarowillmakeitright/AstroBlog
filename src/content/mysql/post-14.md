---
author: Taro Gray
pubDatetime: 2023-11-19T08:43:00.000Z
title: 【MySQL正規形】 第二正規形（2NF）について学ぼう
postSlug: mysql-14
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - MySQL
  - 第2正規形
  - 2NF
  - 正規形
description: "第2正規形（2NF）は、リレーショナルデータベース設計における重要な正規化ステップです。1NF（第一正規形）から一歩進んだ2NFは、データの冗長性をさらに減らし、データ整合性を高めることを目指します。"
---

# 第二正規形（2NF）についての説明

第二正規形（2NF）は、リレーショナルデータベース設計における重要な正規化ステップです。1NF（第一正規形）から一歩進んだ2NFは、データの冗長性をさらに減らし、データ整合性を高めることを目指します。

2NFは、データベースが1NFであることに加えて、非キー属性が主キーに完全に依存していることを要求します。つまり、部分的な依存関係を排除し、各属性が主キー全体に対してのみ関連している状態です。

## 面白いデータを用いた例

想像してみてください：「宇宙探検隊」のデータベースを管理しています。このデータベースには、隊員の個人情報、彼らが参加したミッション、およびそのミッションの詳細が含まれています。

- **非正規形のテーブル**:
  | MemberID | Name | MissionID | MissionName | Destination |
  |----------|---------------|-----------|------------------|-------------|
  | 1 | John Doe | 101 | Jupiter Survey | Jupiter |
  | 2 | Jane Smith | 102 | Mars Colony Prep | Mars |
  | 1 | John Doe | 103 | Saturn Ring Study| Saturn |

このテーブルは2NFを満たしていません。なぜなら、「MissionName」と「Destination」は「MemberID」ではなく、「MissionID」に部分的に依存しているからです。

- **第二正規形のテーブル**:

  - **隊員テーブル**:
    | MemberID | Name |
    |----------|---------------|
    | 1 | John Doe |
    | 2 | Jane Smith |

  - **ミッションテーブル**:
    | MissionID | MissionName | Destination |
    |-----------|------------------|-------------|
    | 101 | Jupiter Survey | Jupiter |
    | 102 | Mars Colony Prep | Mars |
    | 103 | Saturn Ring Study| Saturn |

  - **参加記録テーブル**:
    | MemberID | MissionID |
    |----------|-----------|
    | 1 | 101 |
    | 2 | 102 |
    | 1 | 103 |

第二正規形にすることで、各ミッションの詳細は「ミッションテーブル」で一元管理され、隊員とミッションの関係は「参加記録テーブル」で管理されます。これにより、データの重複が減り、更新の簡素化が図られます。

## まとめ

第二正規形は、データベース設計においてデータの整合性と効率性を高めるために不可欠です。宇宙探検隊の例を通じて、2NFの概念とその重要性を楽しく、わかりやすく伝えることができます。データベースを2NFにすることで、宇宙ミッションのデータ管理がより効果的になります。