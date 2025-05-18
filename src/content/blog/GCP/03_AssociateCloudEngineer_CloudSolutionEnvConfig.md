---
author: Taro Gray
pubDatetime: 2025-05-18T08:00:00.000Z
title: Associate Cloud Engineerの取得に向けた実践問題解析 (クラウド ソリューション環境の設定)
postSlug: 03_AssociateCloudEngineer_CloudSolutionEnvConfig
featured: true
tags:
  - GCP
description: Associate Cloud Engineerの取得に向けた実践問題解析 (クラウド ソリューション環境の設定)
---

## はじめに

この投稿では、Google Cloud Skills Boost の診断問題から「クラウド ソリューション環境の設定」に関する設問を取り上げ、出題形式・選択肢・正解・解説の順で整理しました。Associate Cloud Engineer 認定試験の対策としてご活用ください。

---

## 問題01: OS依存アプリをGCPに移行

**質問**:
Cymbal Superstore はサプライ チェーン アプリケーションを Google Cloud に移行することを決定しました。あなたは特定のオペレーティング システムの依存関係を構成する必要があります。どうすればよいですか？

**選択肢**:

1. Cloud Run でコンテナを使用してアプリケーションを実装する
2. App Engine でコードを使用してアプリケーションを実装する
3. Google Kubernetes Engine でコンテナを使用してアプリケーションを実装する
4. Compute Engine で仮想マシンを使用してアプリケーションを実装する

**正解**: ✅ D

**解説**:
Compute Engine では、OS の選択と構成を自由に行えるため、特定のオペレーティング システム依存の要件に対応できます。

**参照**: Choosing the right compute option in GCP

---

## 問題02: コンテナによる素早いデプロイ

**質問**:
Cymbal Superstore は、旗艦店の POS システム用にクラウド アプリケーションを試験運用することを決定しました。コーディングに集中して迅速にソリューションを開発し、かつポータビリティのあるコードにしたいと考えています。どうすればよいですか？

**選択肢**:

1. Compute Engine VM に SSH 接続し、コードを実行する
2. コードをコンテナ イメージにパッケージ化し、Cloud Run に送信する
3. Google Kubernetes Engine で Deployment マニフェストを実装し、それに対して kubectl apply を実行する
4. Cloud Run functions でソリューションをコーディングする

**正解**: ✅ B

**解説**:
Cloud Run はサーバーレスでコンテナを管理でき、コーディングとデプロイに集中できます。

**参照**: Google Cloud Hosting Options

---

## 問題03: 最小変更でのクラウド移行

**質問**:
高度にカスタマイズされた Ubuntu 上で稼働しているアプリケーションを、コード変更を最小限にしてできるだけ迅速に Google Cloud に移行したいと考えています。どうすればよいですか？

**選択肢**:

1. Compute Engine 仮想マシンを作成し、そのインフラストラクチャにアプリを移行する
2. 既存のアプリケーションを App Engine にデプロイする
3. コンテナ イメージに含めたアプリケーションを Cloud Run にデプロイする
4. Kubernetes クラスタを実装し、Pod を作成してアプリを有効にする

**正解**: ✅ A

**解説**:
Compute Engine は従来のアプリを最小限の変更でクラウドに移行できる最も柔軟な選択肢です。

**参照**: Hosting Options, Compute Engine Docs

---

## 問題05: SQLでの分析クエリ

**質問**:
Cymbal Superstore では、四半期の販売計画を達成しているかどうかを分析する必要があります。このクエリの実行を担当するアナリストは、SQL に馴染みがあります。どのデータ ソリューションを実装すればよいですか？

**選択肢**:

1. BigQuery
2. Cloud SQL
3. Spanner
4. Firestore

**正解**: ✅ A

**解説**:
BigQuery は分析目的で設計された SQL ベースの大規模データウェアハウスです。

**参照**: Cloud Storage Options

---

## 問題06: ホットデータ用ストレージ

**質問**:
Cymbal Superstore のサプライ チェーン アプリケーションでは、大量のデータを頻繁に分析して、ビジネス プロセスと運用ダッシュボードに情報を提供します。このユースケースに適したストレージ クラスはどれですか？

**選択肢**:

1. Archive
2. Coldline
3. Nearline
4. Standard

**正解**: ✅ D

**解説**:
Standard Storage は、頻繁にアクセスする「ホットデータ」に最適なストレージクラスです。

**参照**: Cloud Storage Classes

---

## 問題07: 時系列データとダッシュボード

**質問**:
Cymbal Superstore では、時系列の履歴データを視覚的なダッシュボードに反映する必要があります。これは分析のユースケースです。使用できるストレージ ソリューションを 2 つ選択してください。

**選択肢**:

1. BigQuery
2. Cloud Storage
3. Firestore
4. Cloud SQL
5. Bigtable

**正解**: ✅ A, E

**解説**:
BigQuery は分析用に、Bigtable は時系列データの保存に優れています。

**参照**: Cloud Load Balancing

---

## 問題08: リージョン内での負荷分散

**質問**:
Cymbal Superstore は、ミネソタ州ミネアポリスの旗艦店の e コマース アプリを試験的にアップデート予定です。トラフィックは周辺地域のみで、リソースは us-central1 にあります。このアプリケーション用に、安全で低コストのネットワーク ロード バランシング アーキテクチャを構成するにはどうすればよいですか？

**選択肢**:

1. プレミアム ティアのグローバル外部アプリケーション LB + リージョン内部アプリケーション LB
2. グローバル外部プロキシ ネットワーク LB + プレミアム ティアのパススルー ネットワーク LB
3. スタンダード ティアのリージョン外部アプリケーション LB + リージョン内部アプリケーション LB
4. リージョン内部プロキシ ネットワーク LB + スタンダード ティアの内部プロキシ ネットワーク LB

**正解**: ✅ C

**解説**:
全リソースが同一リージョン内にあり、低コストでセキュアな構成にはリージョンベースのスタンダードティアが最適です。

**参照**: Cloud Load Balancing Overview

---

## 問題09: L7ロードバランサの選択

**質問**:
TCP スタックのレイヤ 7 で実行される Google Cloud のロード バランシング オプションはどれですか？

**選択肢**:

1. グローバル アプリケーション ロードバランサ
2. グローバル プロキシ ネットワーク ロードバランサ
3. リージョン パススルー ネットワーク ロードバランサ
4. リージョン内部プロキシ ネットワーク ロードバランサ

**正解**: ✅ A

**解説**:
グローバル アプリケーション ロードバランサは OSI レイヤ 7 で動作し、HTTP ヘッダーや Cookie に基づいたルーティングが可能です。

**参照**: Cloud Load Balancing Overview

---
