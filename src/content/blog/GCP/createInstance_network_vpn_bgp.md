---
author: Taro Gray
pubDatetime: 2025-06-26T08:00:00.000Z
title: 【GCP】VPNとBGPの作成
postSlug: createInstance_network_vpn_bgp
featured: true
tags:
  - GCP
description: Configuring Google Cloud HA VPNのレッスンにてインスタンスの作成、ネットワークの作成、VPNの作成、BGPの作成を行なった。
---

---

💡 概要

この一連の gcloud コマンドは、以下の手順で カスタム VPCネットワーク を構成しています：1. vpc-demo という名前の カスタムモードの VPCネットワーク を作成 2. それに対して、異なるリージョンに 2つの サブネット を追加

---

🛠 コマンド詳細と解説

1. VPCネットワークの作成（カスタムモード）

```
gcloud compute networks create vpc-demo --subnet-mode custom
```

- vpc-demo という名前の VPC ネットワークを作成
- --subnet-mode custom:

- サブネットは手動で定義するモード（自動では各リージョンに作られない）

---

2. us-west1 にサブネット作成

```
gcloud compute networks subnets create vpc-demo-subnet1 \
--network vpc-demo --range 10.1.1.0/24 --region us-west1
```

- vpc-demo-subnet1: サブネットの名前
- --network vpc-demo: 上で作った VPC に紐づけ
- --range 10.1.1.0/24: このサブネットに割り当てる IP アドレス範囲（CIDR）
- --region us-west1: サブネットが属するリージョン

---

3. us-east1 に別のサブネット作成

```
gcloud compute networks subnets create vpc-demo-subnet2 \
--network vpc-demo --range 10.2.1.0/24 --region us-east1
```

- vpc-demo-subnet2: 別のサブネット
- --range 10.2.1.0/24: 異なる IP 範囲を指定
- --region us-east1: us-east1 リージョンに割り当て

---

🧠 ポイントまとめ

```
用語	説明
VPCネットワーク	論理的なネットワークの器。プロジェクト内の VM やサービスを接続する基盤です。
サブネット	特定のリージョン内で使われる IP 範囲のこと。VPC に属する。
CIDR	IPアドレスとネットマスクをまとめた表記法。例: 10.1.1.0/24（256個のIP）
カスタムモード	自分で必要なリージョン・IP範囲を設定可能。柔軟でセキュア。
```

---

以下は、オンプレミスネットワークを模した VPC 環境構築に使用された gcloud コマンドの記録と、それぞれのオプション・意味の詳細な解説です。

---

🔥 ファイアウォールルールの作成

1. 内部通信 (カスタムトラフィック) を許可

```
gcloud compute firewall-rules create vpc-demo-allow-custom \
  --network vpc-demo \
  --allow tcp:0-65535,udp:0-65535,icmp \
  --source-ranges 10.0.0.0/8
```

🧾 意味と説明: - vpc-demo-allow-custom: ファイアウォールルールの名前 - --network vpc-demo: このルールを適用する VPC 名 - --allow tcp:0-65535,udp:0-65535,icmp:

- 全ての TCP・UDP ポートと ICMP を許可 - --source-ranges 10.0.0.0/8:
- 10.0.0.0 〜 10.255.255.255 の範囲（プライベートIP）からの通信を許可

🔐 主に 内部ネットワークの広範な通信を許可 する目的で使われます。

---

2. SSH と ICMP (ping) を許可

```
gcloud compute firewall-rules create vpc-demo-allow-ssh-icmp \
  --network vpc-demo \
  --allow tcp:22,icmp
```

🧾 意味と説明: - tcp:22: SSH 接続用のポート - icmp: ping に使われるプロトコル

🔐 管理者が VM に SSH 接続したり、ping を使って疎通確認できるようにするルールです。

---

💻 VM インスタンスの作成

3. us-west1-c ゾーンに VM を作成

```
gcloud compute instances create vpc-demo-instance1 \
  --machine-type=e2-medium \
  --zone us-west1-c \
  --subnet vpc-demo-subnet1
```

🧾 意味と説明: - vpc-demo-instance1: インスタンス名 - --machine-type=e2-medium:

- vCPU 2個・メモリ 4GB のインスタンスタイプ - --zone us-west1-c:
- 西海岸リージョンの特定ゾーン - --subnet vpc-demo-subnet1:
- 作成済みのサブネットに属するように指定

---

4. us-east1-d ゾーンに VM を作成

```
gcloud compute instances create vpc-demo-instance2 \
 --machine-type=e2-medium \
 --zone us-east1-d \
 --subnet vpc-demo-subnet2
```

🧾 意味と説明: - vpc-demo-instance2: 別リージョンのインスタンス - --zone us-east1-d:

- 米国東部リージョンの別ゾーン - --subnet vpc-demo-subnet2:
- us-east1 にあるサブネットに属する

---

📌 ポイントまとめ

```
項目	説明
Firewall	TCP/UDP/ICMP を広範囲に許可（内部通信用）＋ 管理アクセス用 SSH/ICMP を個別許可
インスタンス作成	us-west1 と us-east1 の異なるゾーン・サブネットにそれぞれ作成し、リージョン間通信の確認が可能になる構成
セキュリティの原則	最小権限の原則に基づいて、必要な通信のみを明示的に許可するのがベストプラクティス
```

---

以下は、オンプレミスネットワークを模した VPC 環境構築に使用された gcloud コマンドの記録と、それぞれのオプション・意味の詳細な解説です。

---

🌐 1. ネットワークの作成：on-prem

```
gcloud compute networks create on-prem --subnet-mode custom
```

🧾 解説：- on-prem: ネットワーク名。オンプレミス環境を模した名前。- --subnet-mode custom:

- サブネットを自動で作成せず、明示的に定義するカスタムモード。

💡 auto モードだと各リージョンに自動でサブネットが作られますが、custom モードは自分で必要な範囲を定義できます。

---

🧱 2. サブネットの作成

```
gcloud compute networks subnets create on-prem-subnet1 \
  --network on-prem \
  --range 192.168.1.0/24 \
  --region us-west1
```

🧾 解説：- on-prem-subnet1: サブネット名 - --network on-prem: 所属させるVPCネットワーク名 - --range 192.168.1.0/24:

- サブネットのIP範囲（254ホスト分）- --region us-west1:
- このサブネットが存在するリージョン

📌 192.168.0.0/16 はオンプレミスでよく使われるプライベートIP帯。これを模して使用しています。

---

🔥 3. カスタム通信を許可するファイアウォールルール

```
gcloud compute firewall-rules create on-prem-allow-custom \
  --network on-prem \
  --allow tcp:0-65535,udp:0-65535,icmp \
  --source-ranges 192.168.0.0/16
```

🧾 解説：- --allow tcp:0-65535,udp:0-65535,icmp:

- 全ポートのTCP/UDP、ICMP通信を許可 - --source-ranges 192.168.0.0/16:
- 192.168.. のすべてのサブネットからの通信を許可

🔐 内部の広い通信を許可するため、オンプレミス環境でよくある設定です。

---

🔐 4. SSH と ping を許可するファイアウォールルール

```
gcloud compute firewall-rules create on-prem-allow-ssh-icmp \
  --network on-prem \
  --allow tcp:22,icmp
```

🧾 解説：- tcp:22: SSH 接続を許可 - icmp: ping（疎通確認）を許可

💻 管理やモニタリング用途で SSH/ICMP は非常に重要です。

---

💻 5. 仮想マシンの作成

```
gcloud compute instances create on-prem-instance1 \
  --machine-type=e2-medium \
  --zone us-west1-b \
  --subnet on-prem-subnet1
```

🧾 解説：- on-prem-instance1: 作成される仮想マシンの名前 - --machine-type=e2-medium:

- vCPU 2、メモリ 4GB の低コスト・汎用 VM - --zone us-west1-b:
- us-west1 リージョンの特定ゾーン - --subnet on-prem-subnet1:
- 先ほど作成したサブネットに所属させる

---

✅ まとめ表

```
項目	内容
ネットワーク名	on-prem（カスタムモード）
サブネット名	on-prem-subnet1（IP範囲：192.168.1.0/24）
ファイアウォール1	TCP/UDP/ICMP（内部用 192.168.0.0/16）
ファイアウォール2	SSH(22)/ICMP（外部からの管理用）
VM名	on-prem-instance1（us-west1-bゾーン）
```

---

以下は、Google Cloud High Availability (HA) VPN のセットアップに使用された gcloud コマンドの記録と、それぞれのオプションの詳細な解説です。HA VPN は、2つの仮想ゲートウェイ間で高可用性接続を構築するためのサービスです。

---

🛠️ ステップ 1: HA VPN ゲートウェイの作成

VPC 側の VPN ゲートウェイ

```
gcloud compute vpn-gateways create vpc-demo-vpn-gw1 \
  --network vpc-demo \
  --region us-west1
```

オンプレミス側の VPN ゲートウェイ

```
gcloud compute vpn-gateways create on-prem-vpn-gw1 \
  --network on-prem \
  --region us-west1
```

🔍 オプション解説：

オプション 説明
vpn-gateways create HA VPN ゲートウェイを作成するコマンド
--network ゲートウェイを紐づける VPC ネットワーク名
--region ゲートウェイが存在するリージョン。HA VPN はリージョン単位で構成される

💡 HA VPN ゲートウェイは 2 つの外部 IP アドレス（インターフェース）を持ちます。

---

🧾 ステップ 2: ゲートウェイ情報の確認

VPC 側のゲートウェイ情報確認

```
gcloud compute vpn-gateways describe vpc-demo-vpn-gw1 \
  --region us-west1
```

オンプレミス側のゲートウェイ情報確認

```
gcloud compute vpn-gateways describe on-prem-vpn-gw1 \
  --region us-west1
```

🔍 オプション解説：

オプション 説明
vpn-gateways describe 指定した VPN ゲートウェイの詳細情報を表示する
--region 対象となるゲートウェイのリージョン

🔎 ここで表示される IP アドレスやインターフェース情報は、トンネル設定時に必須になります。

---

📡 ステップ 3: Cloud Router の作成

VPC 側のルーター

```
gcloud compute routers create vpc-demo-router1 \
  --region us-west1 \
  --network vpc-demo \
  --asn 65001
```

オンプレミス側のルーター

```
gcloud compute routers create on-prem-router1 \
  --region us-west1 \
  --network on-prem \
  --asn 65002
```

🔍 オプション解説：

オプション 説明
routers create 動的ルーティング用の Cloud Router を作成
--region Cloud Router の設置リージョン
--network ルーターを紐づける VPC
--asn BGP の AS 番号。両端は異なる番号にする必要あり

🚧 BGP（Border Gateway Protocol）でルーティングを自動化するため、Cloud Router は必須です。

---

✅ 全体構成イメージ

┌───────────────────────┐ ┌────────────────────────┐
│ VPC: vpc-demo │ │ On-Prem: on-prem │
│ │ │ │
│ VPN GW: vpc-demo-vpn-gw1 on-prem-vpn-gw1 │
│ └─ Cloud Router: vpc-demo-router1 ─┬─ on-prem-router1 │
│ ASN: 65001 │ ASN: 65002 │
│ Region: us-west1 │ Region: us-west1 │
└───────────────────────┘ └────────────────────────┘

---

💡 次のステップ（まだ未実行）:

次は以下のような設定が必要になります：- VPN トンネルの作成 - BGP セッションの確立 - ルートの確認と疎通確認

---

以下は、あなたが設定した2つのVPNトンネルとルーターのBGPピア構成についての コマンド記録、オプションの詳細、目的の解説です。

---

🔐 VPNトンネルとBGPピアの構成記録と説明（GCP）

前提 - VPNゲートウェイ: vpc-demo-vpn-gw1, on-prem-vpn-gw1 - ルーター: vpc-demo-router1 (ASN: 65001), on-prem-router1 (ASN: 65002) - 共通リージョン: us-west1 - 共通Shared Secret: [SHARED_SECRET] - IP範囲: - 169.254.0.0/30 トンネル0用 - 169.254.1.0/30 トンネル1用

---

🚇 VPNトンネルの作成（片方向ずつ）

VPC - On-Prem トンネル（2本）

```
gcloud compute vpn-tunnels create vpc-demo-tunnel0 \
  --peer-gcp-gateway on-prem-vpn-gw1 \
  --region us-west1 \
  --ike-version 2 \
  --shared-secret [SHARED_SECRET] \
  --router vpc-demo-router1 \
  --vpn-gateway vpc-demo-vpn-gw1 \
  --interface 0
```

```
gcloud compute vpn-tunnels create vpc-demo-tunnel1 \
  --peer-gcp-gateway on-prem-vpn-gw1 \
  --region us-west1 \
  --ike-version 2 \
  --shared-secret [SHARED_SECRET] \
  --router vpc-demo-router1 \
  --vpn-gateway vpc-demo-vpn-gw1 \
  --interface 1
```

---

On-Prem - VPC トンネル（2本）

```
gcloud compute vpn-tunnels create on-prem-tunnel0 \
  --peer-gcp-gateway vpc-demo-vpn-gw1 \
  --region us-west1 \
  --ike-version 2 \
  --shared-secret [SHARED_SECRET] \
  --router on-prem-router1 \
  --vpn-gateway on-prem-vpn-gw1 \
  --interface 0
```

```
gcloud compute vpn-tunnels create on-prem-tunnel1 \
  --peer-gcp-gateway vpc-demo-vpn-gw1 \
  --region us-west1 \
  --ike-version 2 \
  --shared-secret [SHARED_SECRET] \
  --router on-prem-router1 \
  --vpn-gateway on-prem-vpn-gw1 \
  --interface 1
```

---

📡 BGPインターフェースとピアの追加

VPC側ルーターへのインターフェースとピア設定

```
gcloud compute routers add-interface vpc-demo-router1 \
  --interface-name if-tunnel0-to-on-prem \
  --ip-address 169.254.0.1 \
  --mask-length 30 \
  --vpn-tunnel vpc-demo-tunnel0 \
  --region us-west1
```

```
gcloud compute routers add-bgp-peer vpc-demo-router1 \
  --peer-name bgp-on-prem-tunnel0 \
  --interface if-tunnel0-to-on-prem \
  --peer-ip-address 169.254.0.2 \
  --peer-asn 65002 \
  --region us-west1
```

```
gcloud compute routers add-interface vpc-demo-router1 \
  --interface-name if-tunnel1-to-on-prem \
  --ip-address 169.254.1.1 \
  --mask-length 30 \
  --vpn-tunnel vpc-demo-tunnel1 \
  --region us-west1
```

```
gcloud compute routers add-bgp-peer vpc-demo-router1 \
  --peer-name bgp-on-prem-tunnel1 \
  --interface if-tunnel1-to-on-prem \
  --peer-ip-address 169.254.1.2 \
  --peer-asn 65002 \
  --region us-west1
```

---

On-Prem側ルーターへのインターフェースとピア設定

```
gcloud compute routers add-interface on-prem-router1 \
  --interface-name if-tunnel0-to-vpc-demo \
  --ip-address 169.254.0.2 \
  --mask-length 30 \
  --vpn-tunnel on-prem-tunnel0 \
  --region us-west1
```

```
gcloud compute routers add-bgp-peer on-prem-router1 \
  --peer-name bgp-vpc-demo-tunnel0 \
  --interface if-tunnel0-to-vpc-demo \
  --peer-ip-address 169.254.0.1 \
  --peer-asn 65001 \
  --region us-west1
```

```
gcloud compute routers add-interface on-prem-router1 \
  --interface-name if-tunnel1-to-vpc-demo \
  --ip-address 169.254.1.2 \
  --mask-length 30 \
  --vpn-tunnel on-prem-tunnel1 \
  --region us-west1
```

```
gcloud compute routers add-bgp-peer on-prem-router1 \
  --peer-name bgp-vpc-demo-tunnel1 \
  --interface if-tunnel1-to-vpc-demo \
  --peer-ip-address 169.254.1.1 \
  --peer-asn 65001 \
  --region us-west1
```

---

📝 用語と目的まとめ

```
項目	説明
--vpn-gateway	HA VPNのエンドポイント（クラウド側）
--peer-gcp-gateway	相手側VPN Gateway（Google Cloudの場合）
--shared-secret	IKEフェーズ1で使われる事前共有鍵（IPSec）
--router	動的ルーティング（BGP）用のCloud Router
--interface	各トンネルに割り当てる論理インターフェース番号
--ip-address / --peer-ip-address	トンネル間のリンクローカルアドレス（169.254.x.x）
--peer-asn	相手BGPルーターのASN（Autonomous System Number）
```

---

以下は、HA VPN接続後の疎通確認・設定確認・ルーティング調整に使用する gcloud コマンドとそのオプションの意味・目的についての詳細まとめです。

---

🔍 構成確認コマンド

🔸 Cloud Router の状態を確認

```
gcloud compute routers describe vpc-demo-router1 --region us-west1
gcloud compute routers describe on-prem-router1 --region us-west1
```

- 目的: 各 Cloud Router の BGP 状態やインターフェース、ピア設定を確認
- 重要項目: BGP セッションの状態（BGP peer status）、受信経路、広告経路など

---

🔥 ファイアウォールルールの作成

🔹 VPC 側に On-Prem サブネットからの通信を許可

```
gcloud compute firewall-rules create vpc-demo-allow-subnets-from-on-prem \
  --network vpc-demo \
  --allow tcp,udp,icmp \
  --source-ranges 192.168.1.0/24
```

🔹 On-Prem 側に VPC サブネットからの通信を許可

```
gcloud compute firewall-rules create on-prem-allow-subnets-from-vpc-demo \
  --network on-prem \
  --allow tcp,udp,icmp \
  --source-ranges 10.1.1.0/24,10.2.1.0/24
```

- 目的: 各ネットワークが相手のサブネット宛に TCP, UDP, ICMP を通すことを許可
- source-ranges: 許可する送信元の IP レンジ

---

🧭 VPNトンネルの確認

```
gcloud compute vpn-tunnels list
```

- 目的: 作成された VPN トンネルが表示されているか確認

```
gcloud compute vpn-tunnels describe vpc-demo-tunnel0 --region us-west1
gcloud compute vpn-tunnels describe vpc-demo-tunnel1 --region us-west1
gcloud compute vpn-tunnels describe on-prem-tunnel0 --region us-west1
gcloud compute vpn-tunnels describe on-prem-tunnel1 --region us-west1
```

- 目的: 各トンネルのステータス（status: ESTABLISHED など）、トラフィック統計、インターフェース割り当てを確認

---

💻 疎通確認（SSH & ping）

```
gcloud compute ssh on-prem-instance1 --zone zone_name
```

    -	目的: On-Prem ネットワークの VM へ SSH 接続

ping -c 4 10.1.1.2
ping -c 2 10.2.1.2

- 目的: VPC 側のインスタンスに対して On-Prem 側から疎通確認（ICMP）

---

🌐 BGP グローバルモードへの切り替え

```
gcloud compute networks update vpc-demo --bgp-routing-mode GLOBAL
```

- 目的: GCP のネットワークで BGP 経路情報のグローバル共有を有効化
- GLOBAL モードにすることで、すべてのリージョンから広告されたプレフィックスが使用可能になる
- （例：us-west1 のルーターが us-east1 の VM へもルートを広報できる）

---

📘 VPCネットワークの状態確認

```
gcloud compute networks describe vpc-demo
```

- 目的: VPCネットワークの構成と、BGPルーティングモード（REGIONAL or GLOBAL）を確認

---

✅ 補足まとめ

```
コマンド種別	説明
describe	各リソースの構成、状態、関連情報の確認
create firewall-rules	通信制御を明示的に定義（GCPの通信はデフォルト拒否）
ping	通信疎通確認（ICMPが許可されていることが前提）
update --bgp-routing-mode	グローバルルート広告に切り替えたい場合に使用
ssh	仮想マシンに対してGCP経由でアクセス
```

---
