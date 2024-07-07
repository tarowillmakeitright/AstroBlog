---
author: Taro Gray
pubDatetime: 2024-07-07T16:37:00.00Z
title: Proxychainsを使用した匿名ブラウジングの方法
postSlug: cybersecurity-anonymous-browsing-with-proxychains
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Cybersecurity
  - Proxychains
  - Kali Linux
description: Proxychainsを使用して匿名ブラウジングを実現する方法を解説します。Kali Linuxでの設定手順、プロキシサーバーの選択と設定、実際の使用例について詳しく説明します。
---

## 目次

## Proxychainsとは？

Proxychainsは、複数のプロキシサーバーをチェインして、インターネット上での匿名性を高めるためのツールです。これにより、接続元のIPアドレスを隠すことができます。特に、Kali Linuxのようなペネトレーションテスト環境で有用です。

## Kali LinuxでのProxychains設定手順

### 1. プロキシサーバーの選択

まず、いくつかのプロキシサーバーを選択する必要があります。以下の手順で設定を行います。

```sh
sudo updatedb
locate proxychains
```

次に、[https://spys.one/en/](https://spys.one/en/) を開き、プロキシサーバーを3つ選びます。

### 2. Proxychainsの設定ファイルを編集

```sh
sudo nano /etc/proxychains4.conf
```

#### 設定変更内容

1. `#strict_chain` をコメントアウトし、`dynamic_chain` を追加します。
2. `socks4 127.0.0.1 9050` をコメントアウトします。
3. その下に選んだプロキシサーバーのリストを挿入します。

#### 設定ファイル例

```plaintext
# proxychains.conf
#
#       ProxyList format
#       type  host  port [user pass]
#       (values separated by 'tab' or 'blank')
#
#        examples:
#
#           socks5  192.168.67.78   1080    lamer   secret
#           http    192.168.89.3    8080    justu   hidden
#           socks4  192.168.1.49    1080
#           http    192.168.39.93   8080
#
# add proxy here ...
# meanwile
# defaults set to "tor"
#
# socks4 127.0.0.1 9050
#
# dynamic_chain
# Strict_chain
# Quiet_mode
dynamic_chain

# ProxyList format
#       type  host  port [user pass]
http 123.45.67.89 8080
socks5 98.76.54.32 1080
http 234.56.78.90 3128
```

変更を保存し、終了するために `ctrl + x` を押し、`y` と入力して確定します。

### 3. IPアドレスの確認

以下のコマンドを使用して、プロキシチェインを通して接続する前と後のIPアドレスを確認します。

#### 現在のIPアドレスを確認

```sh
curl ifconfig.co
```

#### Proxychainsを使用してFirefoxで確認

```sh
proxychains4 -f /etc/proxychains4.conf firefox
```

Firefoxで [https://ifconfig.co/](https://ifconfig.co/) にアクセスして、表示されるIPアドレスを確認します。

#### Proxychainsを使用してターミナルで確認

```sh
proxychains4 -f /etc/proxychains4.conf curl ifconfig.co
```

このコマンドは、ターミナルでのIPアドレスを表示します。

## 実行結果の比較

Proxychainsを使用する前後で表示されるIPアドレスを比較します。以下のように、Proxychainsを使用することでIPアドレスが変わることを確認できます。

- **Proxychains使用前**: 実際のIPアドレスが表示されます。
- **Proxychains使用後**: 設定したプロキシサーバーのIPアドレスが表示されます。

## まとめ

Proxychainsを使用することで、インターネット上での匿名性を高めることができます。複数のプロキシサーバーをチェインして使用することで、追跡を回避し、プライバシーを保護することが可能です。Kali Linuxでの設定手順と実際の使用例を理解し、セキュリティを強化しましょう。

### 参考文献

- [Proxychains公式ドキュメント](http://proxychains.sourceforge.net/)
- [Kali Linux公式サイト](https://www.kali.org/)
- [Spys.oneプロキシリスト](https://spys.one/en/)
