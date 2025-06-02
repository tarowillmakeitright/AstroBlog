---
author: Taro Gray
pubDatetime: 2025-06-02T08:00:00.000Z
title: GCP VPC と Compute Engine 入門ラボ要約
postSlug: GettingStarted_VPC_and_GCE
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - GCP
description: このハンズオンラボでは、GCP の仮想ネットワーク（VPC）と VM インスタンスの作成・接続性について学びました。以下にポイントを整理します。
---

## GCP VPC と Compute Engine 入門ラボ要約

このハンズオンラボでは、GCP の仮想ネットワーク（VPC）と VM インスタンスの作成・接続性について学びました。以下にポイントを整理します。

⸻

💡 学習ポイント

1. VPC ネットワークとは？

   - GCP における仮想的なネットワーク基盤。
   - サブネット（リージョンごとのネットワークセグメント）で構成。
   - 各プロジェクトにデフォルトで用意され、VM・GKE・App Engine などのリソースの基盤となる。

2. デフォルトネットワークの構成確認

   - 各リージョンにサブネットあり。
   - デフォルトでルートとファイアウォールルール（SSH, RDP, ICMP, Internal）が設定されている。

3. デフォルトネットワークを削除すると…

   - VM は作成できなくなる（ネットワークがないと作成エラーになる）。
   - ルート・ファイアウォールも自動で消える。

4. Auto Mode VPC の再作成と VM 作成

   - 新しく mynetwork を自動モードで作成。
   - 各リージョンに自動的にサブネットが生成される。
   - VM を 2 台作成（us-region / r2-region に 1 台ずつ）。

5. ファイアウォールと接続確認
   - allow-icmp：ping を許可（内部・外部 IP）
   - allow-custom：内部ネットワーク間の通信を許可
   - allow-ssh：SSH 接続を許可

→ 各ルールを削除すると、対応する通信ができなくなる（例：ICMP を削除すると ping ができない）。

⸻

✅ 結論 - VPC ネットワークは GCP 上のすべてのコンピューティングリソースの基盤 - ファイアウォールルールにより通信の制御が可能 - デフォルトネットワークを削除しても、Auto Mode で簡単に再構築可能

⸻

🔗 関連リンク - [VPC ネットワーク概要（公式）](https://cloud.google.com/vpc/docs?hl=ja) - [GCP Compute Engine ドキュメント](https://cloud.google.com/compute/docs?hl=ja)
