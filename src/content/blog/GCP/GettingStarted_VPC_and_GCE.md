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

問題 1

Q: お客様が Preemptible VM（中断可能な仮想マシン）を選ぶ主な理由は何ですか？

選択肢: - A. パフォーマンスを向上させるため - B. プレミアム OS のコストを削減するため - C. コストを削減するため - D. カスタムマシンタイプを使用するため

正解: C

解説:
Preemptible VM（または Spot VM）は、短期的なワークロードに向いており、通常の VM よりも大幅に安価です。プリエンプト（中断）される可能性がある代わりにコストが非常に低いため、コスト削減が主な理由です。

⸻

問題 2

Q: 次のうち、Service Level Agreement（SLA）が提供されているインターコネクトのオプションはどれですか？

選択肢: - A. Carrier Peering - B. Direct Peering - C. Dedicated Interconnect - D. Standard Network Tier

正解: C

解説:
Dedicated Interconnect は Google Cloud とオンプレミス間を直接接続する高帯域・高信頼のサービスで、SLA が提供されます。他のピアリング方法（Carrier Peering や Direct Peering）では SLA がありません。

⸻

問題 3

Q: Google Cloud VPC において、サブネットはどのスコープ（範囲）で定義されますか？

選択肢: - A. グローバル - B. リージョン - C. マルチリージョン - D. ゾーン

正解: B

解説:
VPC サブネットは「リージョン」単位で定義され、同じリージョン内の複数ゾーンにまたがって使用できます。これにより、可用性を高めつつネットワーク設計を簡素化できます。

⸻

問題 4

Q: Cloud Load Balancing は、HTTP ベースのトラフィックをどのように分散しますか？

選択肢: - A. 単一リージョン内の複数の VM 間で分散 - B. 複数の Compute Engine リージョン間で分散 - C. 単一データセンターの物理マシン間で分散 - D. Google Cloud の各種サービス間で分散

正解: B

解説:
Cloud Load Balancing（特にグローバル HTTP(S) ロードバランサ）は、世界中の複数リージョンにまたがってトラフィックを分散できます。これにより、単一のフロントエンドIPアドレスで高速・可用性の高いサービスを実現できます。

---

✅ 結論

- VPC ネットワークは GCP 上のすべてのコンピューティングリソースの基盤 - ファイアウォールルールにより通信の制御が可能 - デフォルトネットワークを削除しても、Auto Mode で簡単に再構築可能

⸻

🔗 関連リンク

- [VPC ネットワーク概要（公式）](https://cloud.google.com/vpc/docs?hl=ja)
- [GCP Compute Engine ドキュメント](https://cloud.google.com/compute/docs?hl=ja)
