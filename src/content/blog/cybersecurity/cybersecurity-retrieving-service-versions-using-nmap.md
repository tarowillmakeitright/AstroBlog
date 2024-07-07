---
author: Taro Gray
pubDatetime: 2024-07-07T16:17:00.00Z
title: Nmapを使用してポートからサービスのバージョンを取得する方法
postSlug: retrieving-service-versions-using-nmap
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Cybersecurity
  - Nmap
  - Network Security
description: Nmapを使用してネットワーク内のサービスのバージョンを特定する方法を解説します。サービスのバージョン情報を取得することで、セキュリティリスクの特定と管理が容易になります。
---

## 目次

## Nmapを使用してポートからサービスのバージョンを取得する方法

ネットワークセキュリティの管理において、ネットワーク内の各サービスのバージョン情報を取得することは重要です。サービスのバージョン情報を把握することで、既知の脆弱性に対する適切な対策を講じることができます。Nmapは、ネットワーク探索およびセキュリティ監査のための強力なツールであり、特定のポート上で実行されているサービスのバージョンを特定するために使用できます。

### サービスバージョン検出の重要性

サービスのバージョン情報を知ることには、以下のような利点があります。

1. **脆弱性の特定**: サービスのバージョン情報を知ることで、既知の脆弱性を特定しやすくなります。
2. **セキュリティパッチの適用**: 古いバージョンのサービスが稼働している場合、適切なセキュリティパッチを適用するための情報が得られます。
3. **ネットワーク管理**: ネットワーク内の全サービスのバージョンを把握することで、ネットワーク管理が効率化されます。

## Nmapの基本的な使い方

Nmapは、様々なネットワークスキャンを実行できる多機能なツールです。以下は、特定のIPアドレスに対してサービスのバージョンを検出するための基本的なコマンドです。

### インストール方法

まず、Nmapをインストールする必要があります。主要なオペレーティングシステムでのインストールコマンドは以下の通りです。

#### Ubuntu/Debian

```sh
sudo apt-get install nmap
```

#### CentOS/RHEL

```sh
sudo yum install nmap
```

#### macOS

```sh
brew install nmap
```

## サービスバージョン検出コマンド

Nmapを使用して特定のIPアドレスのサービスバージョンを検出するには、以下のコマンドを実行します。

```sh
sudo nmap -sV {ipaddress}
```

例えば、`192.168.1.1`のサービスバージョンを検出する場合は、以下のようにコマンドを実行します。

```sh
sudo nmap -sV 192.168.1.1
```

### コマンドの詳細

- **`sudo`**: 管理者権限でコマンドを実行します。
- **`nmap`**: Nmapツールを実行します。
- **`-sV`**: サービスバージョン検出モードを有効にします。
- **`{ipaddress}`**: 対象のIPアドレスを指定します。

### 出力結果の解釈

コマンドを実行すると、Nmapは指定したIPアドレスの各オープンポートで実行されているサービスのバージョン情報を表示します。出力例は以下の通りです。

```plaintext
Starting Nmap 7.91 ( https://nmap.org ) at 2024-06-25 14:25 JST
Nmap scan report for 192.168.1.1
Host is up (0.0010s latency).
Not shown: 995 closed ports
PORT    STATE SERVICE     VERSION
22/tcp  open  ssh         OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
80/tcp  open  http        Apache httpd 2.4.29 ((Ubuntu))
139/tcp open  netbios-ssn Samba smbd 3.X - 4.X (workgroup: WORKGROUP)
445/tcp open  netbios-ssn Samba smbd 4.7.6-Ubuntu (workgroup: WORKGROUP)
```

この出力では、各ポートのサービス名とバージョン情報が表示されています。例えば、ポート22でOpenSSH 7.6p1が実行されていることがわかります。

## 高度なオプション

Nmapには、サービスバージョン検出をさらに詳細に行うための高度なオプションもあります。

### 詳細なスキャン

詳細なスキャンを行うためには、`-A`オプションを使用します。これにより、OS検出やトレースルート情報も取得できます。

```sh
sudo nmap -A 192.168.1.1
```

### 特定のポートを指定

特定のポートのみをスキャンする場合は、`-p`オプションを使用します。

```sh
sudo nmap -sV -p 22,80 192.168.1.1
```

このコマンドは、ポート22と80のサービスバージョンを検出します。

## まとめ

Nmapは、ネットワーク探索およびセキュリティ監査における強力なツールであり、特定のポートで実行されているサービスのバージョン情報を取得するのに非常に有用です。サービスのバージョン情報を把握することで、既知の脆弱性に対する適切な対策を講じることができ、ネットワークのセキュリティを強化することができます。定期的にNmapを使用してネットワークの状態を監視し、セキュリティリスクを早期に発見することをお勧めします。

## 参考文献

- [Nmap公式サイト](https://nmap.org/)
- [Nmapスクリプトエンジン（NSE）](https://nmap.org/book/nse.html)
- [Nmapドキュメンテーション](https://nmap.org/docs.html)
