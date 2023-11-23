---
author: Taro Gray
pubDatetime: 2023-11-16T11:21:00.00Z
title: 【MySQL正規形】第４正規形について学ぼう
postSlug: MySQL-Fourth-Normal-Form
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - MySQL
  - 第4正規形
  - 4NF
  - 正規形
description: 第4正規形（4NF）は、リレーショナルデータベースの設計において、より高度な正規化を行うための概念です。4NFは、特にマルチバリュード依存（多値依存）を排除することに焦点を当てています。これは、ある属性が他の属性に依存し、その依存関係が繰り返し（リピート）されることを防ぐためのものです。"
---

## Table of contents

第4正規形（4NF）は、リレーショナルデータベースの設計において、より高度な正規化を行うための概念です。4NFは、特にマルチバリュード依存（多値依存）を排除することに焦点を当てています。これは、ある属性が他の属性に依存し、その依存関係が繰り返し（リピート）されることを防ぐためのものです。

## 第4正規形（4NF）の条件

- テーブルがボイス・コッド正規形（BCNF）である。
- テーブル内に非自明なマルチバリュード依存が存在しない。

## 面白いデータを用いた例

想像してみてください：「宇宙飛行士」と「惑星探査ミッション」に関するデータベースがあります。各宇宙飛行士が複数の惑星に行き、各惑星には複数の宇宙飛行士が訪れるとします。

- **ミッションテーブル**:
  | Astronaut | Planet |
  |----------------|------------|
  | Neil Armstrong | Moon |
  | Buzz Aldrin | Moon |
  | Yuri Gagarin | Mars |
  | Neil Armstrong | Mars |
  | Buzz Aldrin | Venus |

このテーブルでは、マルチバリュード依存が存在します。例えば、「Neil Armstrong」が「Moon」と「Mars」に行ったという情報が繰り返されています。これは4NFに違反しています。

4NFに準拠するためには、宇宙飛行士と惑星の関連を別々のテーブルに分ける必要があります。例えば、宇宙飛行士ごとに訪れた惑星のリストを保持するテーブルと、惑星ごとに訪れた宇宙飛行士のリストを保持するテーブルを作成します。

## 正規化後のテーブル

- **宇宙飛行士テーブル**:
  | Astronaut | PlanetList |
  |----------------|--------------|
  | Neil Armstrong | Moon, Mars |
  | Buzz Aldrin | Moon, Venus |
  | Yuri Gagarin | Mars |

- **惑星テーブル**:
  | Planet | AstronautList |
  |--------|-----------------------|
  | Moon | Neil Armstrong, Buzz Aldrin |
  | Mars | Neil Armstrong, Yuri Gagarin |
  | Venus | Buzz Aldrin |

こうすることで、各宇宙飛行士が訪れた惑星と、各惑星を訪れた宇宙飛行士という情報が冗長性なく表現できます。4NFは、このように複雑な関連を持つデータを効率的に扱うために役立つ概念です。面白くて実際の例を使うことで、理論をより具体的に理解することができます。
