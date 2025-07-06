---
author: Taro Gray
pubDatetime: 2025-07-06T08:00:00.000Z
title: App Engine Standard と App Enginge Flexible のちがい
postSlug: AppEngine_standard_AppEngine_Flexible
featured: true
tags:
  - GCP
description: Google Cloud の App Engine には 2 つの実行環境があります。
---

Google Cloud の App Engine には 2 つの実行環境があります。

- App Engine Standard
- App Engine Flexible

本記事では、それぞれの違いや使い分けのポイントをまとめます。

---

## 🔍 違いの比較表

| 比較項目       | App Engine Standard              | App Engine Flexible                 |
| -------------- | -------------------------------- | ----------------------------------- |
| 起動時間       | 秒単位（高速）                   | 分単位（遅め）                      |
| スケーリング   | 自動スケーリング（0 に縮退可能） | 自動または手動（0 には縮退不可）    |
| ランタイム     | 管理された固定ランタイム         | カスタムランタイム（Docker 使用可） |
| サポート言語   | Python, Java, Go, PHP など       | ほぼすべての言語（Dockerベース）    |
| SSH アクセス   | 不可                             | 可能                                |
| 永続ディスク   | 使用不可                         | 使用可能                            |
| カスタマイズ性 | 低い                             | 高い                                |
| コスト         | 安価（小規模向け）               | 高め（本番向け）                    |

---

## ✅ 選び方のヒント

| シナリオ                                      | 推奨     |
| --------------------------------------------- | -------- |
| サーバレスで簡単に動かしたい                  | Standard |
| 独自ライブラリを使いたい                      | Flexible |
| Docker イメージで構成したい                   | Flexible |
| ステートレスな API を高速にスケーリングしたい | Standard |
| VM に入ってデバッグ・監視したい               | Flexible |

---

## 📝 まとめ

- **Standard 環境**は「高速・安価・おまかせ」なサーバレスアプリ向け。
- **Flexible 環境**は「自由度が高く本番向け」に適した構成が可能。
