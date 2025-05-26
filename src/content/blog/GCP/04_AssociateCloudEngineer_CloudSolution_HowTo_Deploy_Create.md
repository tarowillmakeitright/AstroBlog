---
author: Taro Gray
pubDatetime: 2025-05-27T08:00:00.000Z
title: クラウド ソリューション䛾デプロイと実装
postSlug: 04_AssociateCloudEngineer_CloudSolution_HowTo_Deploy_Create
featured: true
tags:
  - GCP
description: クラウド ソリューション䛾デプロイと実装
---

## はじめに

Google Cloud Skills Boostの試験問題「クラウド ソリューションのデプロイと実装」を通して、Associate Cloud Engineer 試験の中核部分を学びました。
本記事は、問題と選択肢、正解とその理由をまとめ、複素なデプロイシナリオに対する理解を添えています。

---

## 問題01: MySQL データベースの移行

**質問**:
Cymbal Superstore の営業部門には中規模の MySQL データベースがあります。このデータベースにはユーザー定義関数が含まれており、マーケティング部門が内部利用しています。最もスピーディかつ経済的に Google Cloud に移行するには、どうすればよいでしょうか？

**選択肢**:

1. Cloud Marketplace で MySQL のマシンイメージを見つけ、ニーズを満たすように構成する
2. Cloud SQL を使用してデータベース インスタンスを実装し、ローカルデータをバックアップして復元する
3. N2 マシンタイプで Compute Engine VM を構成し、MySQL をインストールしてデータを復元する
4. gcloud を使用して E2-standard-8 マシンタイプで Compute Engine インスタンスを構成し、MySQL をインストールする

**正解**: ✅ C

**解説**:
Cloud SQL はユーザー定義関数をサポートしておらず、Compute Engine VM を利用することで柔軟な構成とコストのバランスを確保できます。特に N2 マシンタイプは中規模システムに最適です。

---

## 問題02: MIGでのOS自動更新

**質問**:
Cymbal Superstore の e コマース システムはマネージド インスタンス グループ（MIG）上に構成されています。最小限のリソースで OS を自動的に更新したいとき、どのように構成すればよいでしょうか？

**選択肢**:

1. 追従型更新を使って VM を更新する
2. 先行型更新を使って VM を更新する
3. 最大サージを 5 に設定して更新する
4. 既存のインスタンスを放棄してテンプレートを作り直す

**正解**: ✅ B

**解説**:
先行型更新は、段階的に OS を更新しつつ、使用リソースを最小限に抑えるローリングアップデート戦略に対応しています。追従型ではインタラクティブ更新ができないため不向きです。

---

## 問題03: 小規模 Kubernetes クラスタの構成

**質問**:
サプライチェーンプロジェクトの開発チームがパイロット環境用に小規模な Kubernetes クラスタを使ってクラウドアプリを構築し始めています。チームメンバー限定でアクセスし、高可用性は不要です。どのようにクラスタを構成するのが最適でしょうか？

**選択肢**:

1. Autopilot クラスタ（us-central1-a, Ubuntu）
2. 限定公開の Standard ゾーンクラスタ（us-central1-a, Ubuntu）
3. Standard リージョンクラスタ（us-central1, コンテナ最適化イメージ）
4. Autopilot クラスタ（us-central1, Ubuntu）

**正解**: ✅ B

**解説**:
Standard ゾーンクラスタであれば、小規模環境に適しており、Ubuntu ベースの VM を使って柔軟な操作が可能です。Autopilot はリソース管理の自由度が低く、要件に合いません。

---

## 問題04: コンテナアプリの最適なホスティング

**質問**:
コンテナ化された Web アプリを迅速にデプロイし、インフラ管理不要でリクエスト時のみ課金される環境が求められています。また、カスタムパッケージのサポートも必要です。最適なサービスはどれですか？

**選択肢**:

1. App Engine フレキシブル環境
2. App Engine スタンダード環境
3. Cloud Run
4. Cloud Run functions

**正解**: ✅ C

**解説**:
Cloud Run はフルマネージドのサーバーレス環境で、コンテナ単位のデプロイが可能です。カスタムパッケージも利用でき、スケーラビリティやコスト効率の面でも優れています。

---

## 問題05: Cloud Storageトリガーの設定

**質問**:
Cloud Storage バケットに追加されるファイルを分析・処理する必要があります。プログラミング チームは Python に精通しています。分析時間は最長で 5 分です。Cloud Run functions で関数を実装する際、`gcloud` の `--trigger-event` パラメータはどのように構成すべきですか？

**選択肢**:

1. --trigger-event google.storage.object.finalize
2. --trigger-event google.storage.object.create
3. --trigger-event google.storage.object.change
4. --trigger-event google.storage.object.add

**正解**: ✅ 1. --trigger-event google.storage.object.finalize

**解説**:
Cloud Storage に対するオブジェクトの書き込みが完了したタイミングでトリガーされるイベントは `finalize` です。

---

## 問題06: CLIによるCloud Storageバケット作成

**質問**
ニューヨーク市とサンフランシスコのユーザーにサービスを提供する Cloud Storage バケットが必要です。ロンドンのユーザーは使用しません。ACL の使用は計画していません。どの CLI コマンドを使用しますか？

**選択肢**:

1. --remove-acl-grant を指定して、gcloud storage objects コマンドを実行する
2. マルチリージョンのロケーションを指定し、ACL 評価をオフにするオプションを指定して、gsutil mb コマンドを実行する
3. --location を指定せずに gcloud storage buckets create コマンドを実行する
4. --placement us-east1, europe-west2 を指定して、gcloud storage buckets create コマンドを実行する

**正解**: ✅ 3. --location を指定せずに gcloud storage buckets create コマンドを実行する

**解説**:
ロケーションを指定しない場合は、米国マルチリージョンがデフォルトで使用されます。これはニューヨークとサンフランシスコに適しています。

---

## 問題07: Cloud SQLのフェイルオーバー構成

**質問**:
Cloud SQL を使ってサプライ チェーン アプリケーションのデータベース バックエンドを構成します。ゾーン障害に備えた自動フェイルオーバーの設定を行うには、`gcloud sql instances create` コマンドでどの引数を指定する必要がありますか？

**選択肢**:

1. --availability-type
2. --replica-type
3. --secondary-zone
4. --master-instance-name

**正解**: ✅ 1. --availability-type

**解説**:
この引数により、リージョン可用性の設定ができ、自動フェイルオーバーが有効化されます。

---

## 問題08: Cloud StorageからBigQueryへのデータ転送

**質問**:
Cloud Storage に 1 時間おきに取り込まれるデータを BigQuery に読み込みたい。最小限のコストと手順で実装するには？

**選択肢**:

1. bq load コマンドを cron でスケジュール
2. BigQuery ストリーミング API を使用
3. Cloud Run functions + Dataflow パイプラインを使用
4. BigQuery Data Transfer Service を使用

**正解**: ✅ 4. BigQuery Data Transfer Service を使用

**解説**:
BigQuery Data Transfer Service は簡単なスケジューリングで Cloud Storage と BigQuery の統合が可能です。

---

## 問題09: VPCの構成管理

**質問**:
IP 範囲やサブネットの構成を完全に制御できる VPC ネットワークの種類は？

**選択肢**:

1. プロジェクトのデフォルト ネットワーク
2. 自動モード ネットワーク
3. カスタムモード ネットワーク
4. カスタム ネットワークに変換された自動モード ネットワーク

**正解**: ✅ 3. カスタムモード ネットワーク

**解説**:
カスタムモードでは、IP 範囲やサブネットの場所を明示的に指定でき、細かい構成が可能です。

---

## 問題10: terraform apply の挙動

**質問**:
terraform apply コマンドを実行すると何が起こるか？

**選択肢**:

1. 最新バージョンの Terraform プロバイダがダウンロードされる
2. 構成ファイルの構文が検証される
3. 作成されるリソースのプレビューが表示される
4. リクエストされたリソースが設定される

**正解**: ✅ 4. リクエストされたリソースが設定される

**解説**:
terraform apply は、構成ファイルの内容に基づいて実際にクラウドリソースを作成・変更します。
