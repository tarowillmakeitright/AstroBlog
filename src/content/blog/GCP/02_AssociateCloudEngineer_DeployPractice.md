---
author: Taro Gray
pubDatetime: 2025-05-18T08:00:00.000Z
title: Associate Cloud Engineerの取得に向けた実践問題解析 (GCP デプロイと実装)
postSlug: 02_AssociateCloudEngineer_DeployPractice
featured: true
tags:
  - GCP
description: クラウド ソリューションのデプロイと実装
---

## はじめに

Google Cloud Skills Boostの試験問題「クラウド ソリューションのデプロイと実装」を通して、Associate Cloud Engineer 試験の中核部分を学びました。
本記事は、問題と選択肢、正解とその理由をまとめ、複素なデプロイシナリオに対する理解を添えています。

---

## 問題01: MIGでOSを自動更新

**質問**:
Cymbal Superstore の e コマース システムのバックエンドは、マネージド インスタンス グループで構成されています。使用するリソースを最小限に押さえつつ、インスタンスのOSを自動で更新する必要があります。どうすればよいでしょうか。

**選択肢**:

1. 新しいインスタンス テンプレートを作成する。\[VM を更新]をクリックする。更新タイプを \[追従型] に設定する。\[起動]をクリックする。
2. マネージド インスタンス グループ内の各インスタンスを放棄する。インスタンス テンプレートを削除して新しいテンプレートと置き換え、マネージド グループでインスタンスを再作成する。
3. 新しいインスタンス テンプレートを作成し、\[VM を更新]をクリックする。更新タイプを \[先行型] に設定する。\[起動]をクリックする。
4. 新しいインスタンス テンプレートを作成する。\[VM を更新]をクリックする。最大サージを 5 に設定する。\[起動]をクリックする。

**正解**: ✅ C

**解説**:
\[先行型]更新は、段階的にインスタンスを先に作成してから旧インスタンスを削除する戦略であり、ダウンタイムを最小限にしながらOS更新を行うのに最適です。

---

## 問題02: Cloud SQL 移行に関する制約

**質問**:
Cymbal Superstore の営業部門には中規模の MySQL データベースがあります。このデータベースにはユーザー定義関数が含まれており、すばやくかつ経済的に Google Cloud へ移行したいと求められています。どうすればよいですか？

**選択肢**:

1. gcloud を使用して E2-standard-8 マシンタイプで Compute Engine インスタンスを実装し、MySQL をインストールして構成する。
2. Cloud Marketplace で MySQL のマシンイメージを見つけ、ニーズを満たすように構成する。
3. Cloud SQL を使用してデータベース インスタンスを実装し、ローカルデータをバックアップして新しいインスタンスに復元する。
4. N2 マシンタイプで Compute Engine VM を構成し、MySQL をインストールして、新しいインスタンスにデータを復元する。

**正解**: ✅ A

**解説**:
Cloud SQL はユーザー定義関数（UDF）をサポートしておらず、MySQL の完全な互換性が求められる場合は Compute Engine 上での手動構成が現実的です。

---

## 問題03: Cloud SQL の高可用性

**質問**:
Cloud SQL で自動フェイルオーバーを構成するには、gcloud sql instances create コマンドセットでどの引数を指定すべきですか？

**選択肢**:

1. --master-instance-name
2. --availability-type
3. --secondary-zone
4. --replica-type

**正解**: ✅ B

**解説**:
`--availability-type=REGIONAL` を指定することで、高可用性（HA）構成が可能となり、ゾーン障害時に自動でフェイルオーバーします。

---

## 問題04: Cloud Run での迅速なデプロイ

**質問**:
カスタムパッケージを含むコンテナ化されたウェブアプリケーションをインフラ管理不要でデプロイし、リクエスト単位の従量課金にしたい。どのサービスが最適ですか？

**選択肢**:

1. App Engine フレキシブル環境
2. Cloud Run functions
3. Cloud Run
4. App Engine スタンダード環境

**正解**: ✅ C

**解説**:
Cloud Run はフルマネージドなサーバーレスサービスで、Docker コンテナを実行でき、HTTP リクエストごとに課金されます。カスタムライブラリにも対応しています。

---

## 問題05: terraform apply の動作

**質問**:
terraform apply コマンドで実行されるアクションは何ですか？

**選択肢**:

1. Terraform の構成ファイルの構文が検証される
2. 作成されるリソースのプレビューが表示される
3. 最新バージョンの Terraform プロバイダがダウンロードされる
4. Terraform の構成ファイルでリクエストされたリソースが設定される

**正解**: ✅ D

**解説**:
`terraform apply` は実際にリソースを作成・変更・削除するコマンドで、構成ファイル通りにインフラが適用されます。

---

## 問題06: BigQuery への定期データロード

**質問**:
Cloud Storage に毎時間アップロードされるデータを、最小のコストで BigQuery にロードするにはどうすればよいですか？

**選択肢**:

1. プログラムで BigQuery のストリーミング API を使用してバケットからデータを読み取る
2. Cloud Run functions の関数を作成して、Dataflow パイプライン経由で BigQuery にデータを push する
3. BigQuery Data Transfer Service を使用して、バケットと BigQuery の間の転送をスケジュール設定する
4. コマンドライン スクリプトで bq load コマンドを実装し、cron を使用してスケジュール設定する

**正解**: ✅ C

**解説**:
BigQuery Data Transfer Service は自動スケジュールに対応し、手軽にコスト効率よく Cloud Storage との連携が可能です。

---

## 問題07: Cloud Storage トリガーイベント

**質問**:
Cloud Storage にオブジェクトが追加された際に Cloud Functions をトリガーするには、--trigger-event にどの値を指定しますか？

**選択肢**:

1. google.storage.object.add
2. google.storage.object.finalize
3. google.storage.object.change
4. google.storage.object.create

**正解**: ✅ B

**解説**:
`google.storage.object.finalize` は、オブジェクトの書き込み完了後に発生するイベントで、分析や処理トリガーに最適です。

---

## 問題08: 限定公開のクラスタ構成

**質問**:
サプライチェーンアプリ用の小規模 Kubernetes クラスタを us-central1-a に実装し、チーム内限定で利用可能とする場合、どの構成が最適ですか？

**選択肢**:

1. デフォルトプールと Ubuntu イメージで Autopilot クラスタを us-central1-a に実装
2. Ubuntu イメージタイプで Autopilot クラスタを us-central1 に実装
3. デフォルトプールと Ubuntu イメージで限定公開の Standard ゾーンクラスタを us-central1-a に実装
4. デフォルトプールとコンテナ最適化イメージで限定公開の Standard リージョンクラスタを us-central1 に実装

**正解**: ✅ C

**解説**:
Standard ゾーンクラスタは制御性が高く、小規模かつチーム内専用のクラスタ構成に適しています。

---

## 問題09: VPC のカスタム構成

**質問**:
IP 範囲やリージョンごとのサブネットを完全に制御したい場合、どの VPC 構成が適切ですか？

**選択肢**:

1. 自動モードネットワーク
2. カスタムモードネットワーク
3. カスタムネットワークに変換された自動モードネットワーク
4. プロジェクトのデフォルトネットワーク

**正解**: ✅ B

**解説**:
カスタムモードネットワークでは、サブネットや IP 範囲を手動で定義でき、きめ細かなネットワーク設計が可能です。

---

## 問題10: Cloud Storage CLI の選定

**質問**:
NYC と SF のユーザーに対応し、ACL を使わない Cloud Storage バケットを CLI で作成したい。どのコマンドが適切ですか？

**選択肢**:

1. --placement us-east1, europe-west2 を指定して、gcloud storage buckets create を実行
2. --remove-acl-grant を指定して、gcloud storage objects を実行
3. --location を指定せずに gcloud storage buckets create を実行
4. マルチリージョンロケーションと ACL 評価オフオプションを指定して、gsutil mb を実行

**正解**: ✅ D

**解説**:
`gsutil mb -l US` などの形式でマルチリージョン指定が可能です。ACL 無効化もオプション設定で対応できます。

---
