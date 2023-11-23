---
author: Taro Gray
pubDatetime: 2023-11-16T11:21:00.000Z
title: 【MySQL正規形】第５正規形について学ぼう
postSlug: post-17
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - MySQL
  - 第5正規形
  - 5NF
  - 正規形
description: "第５正規形（5NF）、またはプロジェクション・ジョイン正規形（PJNF）は、リレーショナルデータベース設計における最も高度な正規化の形態の一つです。5NFは、ジョイン依存性を完全に理解し、データの冗長性を極力排除することに焦点を当てています。"
---

## Table of contents

第五正規形（5NF）、またはプロジェクション・ジョイン正規形（PJNF）は、リレーショナルデータベース設計における最も高度な正規化の形態の一つです。5NFは、ジョイン依存性を完全に理解し、データの冗長性を極力排除することに焦点を当てています。

## 第五正規形（5NF）の条件

- テーブルが第四正規形（4NF）である。
- テーブル内のすべてのジョイン依存が、その候補キーによってのみ生成される。

## 面白いデータを用いた例

想像してみてください：「ハッカーグループ」と「攻撃ターゲット」、「使用ツール」に関するデータベースがあります。各ハッカーグループが特定のターゲットに対して特定のツールを使用するとします。

- **ハッキングミッションテーブル**:
  | GroupName | Target | Tool |
  |---------------|------------|-------------|
  | CyberWolves | Server | SQLi |
  | CyberWolves | Server | Ransomware |
  | PhantomHack | Database | SQLi |
  | PhantomHack | Email | Phishing |
  | CyberWolves | Email | Phishing |

このテーブルでは、複雑な関連が存在します。例えば、「CyberWolves」が「Server」に対して「SQLi」や「Ransomware」を使用するという情報があります。これは5NFに違反する可能性があります。

5NFに準拠するためには、この複雑な関連をよりシンプルな関連に分割する必要があります。これにより、データの重複を減らし、更新時の問題を防ぐことができます。

## 正規化後のテーブル

- **ハッカーグループとターゲットテーブル**:
  | GroupName | Target |
  |---------------|------------|
  | CyberWolves | Server |
  | PhantomHack | Database |
  | PhantomHack | Email |
  | CyberWolves | Email |

- **ハッカーグループとツールテーブル**:
  | GroupName | Tool |
  |---------------|-------------|
  | CyberWolves | SQLi |
  | CyberWolves | Ransomware |
  | PhantomHack | SQLi |
  | PhantomHack | Phishing |

- **ターゲットとツールテーブル**:
  | Target | Tool |
  |---------------|-------------|
  | Server | SQLi |
  | Server | Ransomware |
  | Database | SQLi |
  | Email | Phishing |

これらのテーブルにより、各ハッカーグループがどのターゲットにどのツールを使用するかが一意に決定され、冗長性が大幅に減少します。また、新しいターゲットやツールが追加された場合のデータの整合性も保たれやすくなります。

5NFは、データベースの複雑な関係をシンプルに保ち、効率的なデータ操作を可能にします。面白くて実際の例を使うことで、この高度な概念をより具体的に理解することができます。
