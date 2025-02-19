---
author: Taro Gray
pubDatetime: 2025-01-31T08:00:00.000Z
title: Lpic1 GNUとLinuxコマンド（主題103）編
postSlug: linux-lpic1-gui-command
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
description: Lpic1 GNUとLinuxコマンド（主題103）編
---

## Table of contents

## Man 1-9 ってどういう時に使うの

man 1-9 は、Linux の man（マニュアル）コマンドの セクション番号 を指定して特定のカテゴリのマニュアルページを表示するために使います。

1. man コマンドのセクションとは？

man ページは 9つのセクション に分類されており、それぞれ異なる種類の情報を提供します。

セクション番号 内容
1 ユーザーが実行できるコマンド（例: ls, cd, echo）
2 システムコール（カーネルが提供する関数）
3 ライブラリ関数（C言語の標準ライブラリなど）
4 デバイスファイル（例: /dev/null）
5 設定ファイルのフォーマットや構造（例: /etc/passwd）
6 ゲーム（例: fortune, rogue）
7 マクロパッケージやその他の特別なトピック（例: man 7 regex）
8 システム管理用コマンド（例: shutdown, iptables）
9 カーネル内部（開発者向けの情報）

2. man セクションの指定方法

a. man だけを実行

man printf

デフォルトでは セクション1（ユーザーコマンド） の printf を表示します。

b. 特定のセクションを指定

例: man 1 printf

man 1 printf

→ printf コマンド（ユーザーコマンド）のマニュアルを表示。

例: man 3 printf

man 3 printf

→ printf の C言語のライブラリ関数（stdio.h）の説明を表示。

違いを確認

man 1 printf
man 3 printf

    •	man 1 printf → シェルの printf コマンド
    •	man 3 printf → C言語の printf 関数

3. man セクションを使う理由
   1. 同じ名前のコマンドと関数を区別
      • 例: open

man 1 open # コマンド
man 2 open # システムコール

    •	man 1 open → open コマンドの説明
    •	man 2 open → open() システムコール（ファイルを開く）の説明

    2.	カーネルやライブラリ関数を調査
    •	man 2 read → read() システムコール
    •	man 3 read → read() ライブラリ関数（glibc）
    3.	設定ファイルの詳細を調べる

man 5 passwd → /etc/passwd のフォーマットを確認。 4. man -k を使ってセクションを検索 特定のキーワードがどのセクションにあるかを調べるには：
man -k printf

出力例:

printf (1) - format and print data
printf (3) - formatted output conversion

→ printf はセクション 1 と 3 にあることがわかる。

5. まとめ

コマンド 説明
man 1 ls ls コマンドのマニュアルを表示
man 2 open open() システムコールのマニュアル
man 3 printf printf() ライブラリ関数の説明
man 5 passwd /etc/passwd 設定ファイルのフォーマット
man -k printf どのセクションにあるか検索

man のセクションを理解すると、より正確に必要な情報を取得できます！ 😊

## Tr alpha digit lower upper alnum spaceを説明して

tr コマンドは、文字の変換や削除、圧縮を行うコマンド です。
シェルスクリプトやコマンドラインでの文字列処理に役立ちます。

1. tr コマンドの基本構文

tr [オプション] セット1 [セット2]

    •	セット1: 変換したい文字の範囲
    •	セット2: 変換後の文字の範囲（省略可）

2. tr の主要な文字クラス

文字クラス（[:クラス名:]）を使うと、特定の種類の文字を対象にできます。

クラス名 説明 例
alpha アルファベット（a-z, A-Z） [[:alpha:]]
digit 数字（0-9） [[:digit:]]
lower 小文字（a-z） [[:lower:]]
upper 大文字（A-Z） [[:upper:]]
alnum 英数字（a-z, A-Z, 0-9） [[:alnum:]]
space スペース・タブ・改行 [[:space:]]

3. tr の使用例

(1) 小文字を大文字に変換

echo "hello world" | tr '[:lower:]' '[:upper:]'

出力:

HELLO WORLD

[:lower:] → [:upper:] に変換

(2) 数字を # に置き換える

echo "Phone: 123-456-7890" | tr '[:digit:]' '#'

出力:

Phone: ###-###-####

[:digit:] → # に変換

(3) スペースを \_ に置き換える

echo "This is a test" | tr '[:space:]' '\_'

出力:

This_is_a_test

[:space:] → \_ に変換

(4) 大文字を小文字に変換

echo "HELLO WORLD" | tr '[:upper:]' '[:lower:]'

出力:

hello world

[:upper:] → [:lower:] に変換

(5) 英数字以外の文字を削除

echo "Hello@123!" | tr -d '[:alnum:]'

出力:

@!

説明:
• -d オプションは 削除（delete）。
• [:alnum:] は 英数字（a-z, A-Z, 0-9）。
• つまり、英数字を削除し、@! だけが残る。

4. tr のオプション

オプション 説明
-d 指定した文字を削除
-s 連続した文字を1つに圧縮
-c 指定した文字 以外 を対象にする

(6) 連続するスペースを1つに圧縮

echo "This is a test" | tr -s '[:space:]'

出力:

This is a test

説明:
• -s で 連続するスペースを1つに圧縮。

(7) 英字以外の文字を削除

echo "Hello123@World!" | tr -d -c '[:alpha:]'

出力:

HelloWorld

説明:
• -d で 削除。
• -c で [:alpha:] 以外 を削除（123@! は消える）。

5. まとめ

クラス名 説明 例
alpha アルファベット（a-z, A-Z） [[:alpha:]]
digit 数字（0-9） [[:digit:]]
lower 小文字（a-z） [[:lower:]]
upper 大文字（A-Z） [[:upper:]]
alnum 英数字（a-z, A-Z, 0-9） [[:alnum:]]
space スペース・タブ・改行 [[:space:]]

💡 ポイント
• tr '[:lower:]' '[:upper:]' → 小文字 → 大文字
• tr '[:digit:]' '#' → 数字 → #
• tr -d '[:alnum:]' → 英数字以外を削除
• tr -s '[:space:]' → 連続するスペースを1つに圧縮

tr コマンドを使うと、シンプルな文字変換が簡単にできるので、シェルスクリプトなどで活用できます！ 😊

## etc/fstabのマウントオプションについてそれぞれ簡潔に説明して

Async
Auto
No auto
Defaults
Exec
Noexec
Ro
Rw
Suid
User
Users
Nouser

/etc/fstab の マウントオプション は、システム起動時や mount コマンド実行時の動作を制御する設定です。以下、それぞれのオプションについて簡潔に説明します。

1. async
   • 非同期モード（書き込みが即座にディスクに反映されず、バッファリングされる）
   • 利点: 高速化
   • 欠点: システムクラッシュ時にデータ消失のリスク

2. auto
   • mount -a 実行時に 自動的にマウント される
   • デフォルトで有効

3. noauto
   • 手動でのみマウント可能（mount -a やブート時に自動マウントされない）

4. defaults
   • 標準的なオプションセット（rw, suid, dev, exec, auto, nouser, async）を適用

5. exec
   • 実行ファイルを許可（ディスク上のバイナリを実行可能）

6. noexec
   • 実行ファイルを禁止（セキュリティ向上のため、/tmp などに推奨）

7. ro（read-only）
   • 読み取り専用（書き込み禁止）

8. rw（read-write）
   • 読み書き可能

9. suid
   • SUID/SGID ビットを許可
   • 一部のプログラムが 所有者の権限で実行可能（ping など）

10. nosuid
    • SUID/SGID を無効化（セキュリティ向上）

11. user
    • 一般ユーザーがマウント可能
    • ただし、そのユーザーのみアンマウント可能

12. users
    • 一般ユーザーがマウント可能
    • 他のユーザーもアンマウント可能

13. nouser
    • 一般ユーザーによるマウント禁止
    • デフォルト設定

💡 まとめ

オプション 説明
async 非同期書き込み（データバッファリング）
auto システム起動時に自動マウント
noauto 手動マウントのみ
defaults 一般的なオプションセット
exec バイナリ実行許可
noexec バイナリ実行禁止（セキュリティ向上）
ro 読み取り専用
rw 読み書き可能
suid SUID/SGID を許可
nosuid SUID/SGID を無効化
user 一般ユーザーがマウント可（本人のみアンマウント可）
users 一般ユーザーがマウント可（他のユーザーもアンマウント可）
nouser 一般ユーザーのマウント禁止（デフォルト）

各オプションは、用途やセキュリティ要件に応じて適切に設定してください！ 😊

## Cut -c -d -fオプションについて簡潔に書いて

cut コマンドは、テキストデータから特定の部分を抽出するために使用されます。
主要なオプション -c, -d, -f の説明を簡潔にまとめます。

1. -c（指定した 文字位置 を抽出）

echo "abcdef" | cut -c 2-4

出力:

bcd

説明:
• -c 2-4 → 2文字目から4文字目を抽出

2. -d（フィールドの 区切り文字 を指定）

echo "apple,banana,grape" | cut -d ',' -f 2

出力:

banana

説明:
• -d ',' → , を区切り文字としてフィールドを分割
• -f 2 → 2番目のフィールドを取得

3. -f（指定した フィールド番号 を抽出）

echo "name age country" | cut -d ' ' -f 1,3

出力:

name country

説明:
• -d ' ' → スペースを区切り文字に
• -f 1,3 → 1番目と3番目のフィールドを取得

💡 まとめ

オプション 説明 例
-c 指定した文字の範囲を抽出 cut -c 1-3 file.txt
-d 区切り文字を指定 cut -d ',' -f 2 file.txt
-f 指定したフィールドを抽出 cut -f 1,3 -d ' '

-c は文字単位、-d & -f はフィールド単位で抽出する点がポイントです！ 😊

## Netstat -a -t -u -4 -6 -p -l -nのオプションについてそれぞれ簡潔に説明して

netstat コマンドは、ネットワークの接続状況を確認するために使用されます。
主要なオプション -a, -t, -u, -4, -6, -p, -l, -n の説明を簡潔にまとめます。

1. -a（全ての接続を表示）

netstat -a

    •	確立済み（ESTABLISHED）と待機中の接続をすべて表示。
    •	リスニング（LISTEN）中のポートも表示。

2. -t（TCP 接続のみ表示）

netstat -t

    •	TCP（Transmission Control Protocol）接続のみ表示。

3. -u（UDP 接続のみ表示）

netstat -u

    •	UDP（User Datagram Protocol）接続のみ表示。

4. -4（IPv4 のみ表示）

netstat -4

    •	IPv4（例: 192.168.1.1）のみ表示。

5. -6（IPv6 のみ表示）

netstat -6

    •	IPv6（例: fe80::1）のみ表示。

6. -p（プロセス情報を表示）

netstat -p

    •	どのプロセスがポートを使用しているかを表示。
    •	管理者権限（sudo）が必要。

7. -l（リスニングポートのみ表示）

netstat -l

    •	現在リスニング中（待機中）のポートのみ表示。
    •	通信待ちのサーバープロセスを確認する際に便利。

8. -n（アドレスとポートを数値で表示）

netstat -n

    •	ホスト名の逆引き（DNS解決）をせず、数値アドレスで表示。
    •	表示速度が速くなる。

9. オプションの組み合わせ例

(1) リスニング中の TCP/UDP ポートを表示

netstat -tuln

説明:
• -t → TCP
• -u → UDP
• -l → リスニング中
• -n → 数値アドレス表示

(2) プロセスごとの使用ポートを確認

sudo netstat -tulpn

説明:
• -t → TCP
• -u → UDP
• -l → リスニング中
• -p → プロセス情報
• -n → 数値表示

💡 まとめ

オプション 説明
-a すべての接続を表示（確立済み + リスニング）
-t TCP接続のみ表示
-u UDP接続のみ表示
-4 IPv4 のみ表示
-6 IPv6 のみ表示
-p 使用中のプロセスを表示（要 sudo）
-l リスニング中のポートのみ表示
-n DNS解決せず数値で表示（高速化）

特定の接続を絞り込む場合、オプションを組み合わせると効果的です！ 😊

## Ss についてメモ

すべての TCP ソケットをサービス名と共に表示する:
$ ss -at
すべての TCP ソケットをポート番号と共に表示する:
$ ss -atn
すべての UDP ソケットを表示する:
$ ss -au

ss コマンドのメモ（ネットワークソケット情報の表示）

ss コマンドは netstat の高速な代替ツールで、ネットワークソケットの状態を確認するのに使用されます。

1. すべての TCP ソケットをサービス名と共に表示

ss -at

    •	-a → すべてのソケット（リスニング + 確立済み）を表示
    •	-t → TCPソケットのみを表示

例:

State Recv-Q Send-Q Local Address:Port Peer Address:Port
LISTEN 0 128 0.0.0.0:ssh 0.0.0.0:\*
ESTABLISHED 0 0 192.168.1.100:ssh 192.168.1.50:51123

ポイント:
• ssh のようにサービス名が表示される。

2. すべての TCP ソケットをポート番号と共に表示

ss -atn

    •	-a → すべてのソケットを表示
    •	-t → TCPソケットのみを表示
    •	-n → 数値表示（ホスト名・サービス名を解決しない）

例:

State Recv-Q Send-Q Local Address:Port Peer Address:Port
LISTEN 0 128 0.0.0.0:22 0.0.0.0:\*
ESTABLISHED 0 0 192.168.1.100:22 192.168.1.50:51123

ポイント:
• 22 のようにポート番号が直接表示される（サービス名ではなく数値）。

3. すべての UDP ソケットを表示

ss -au

    •	-a → すべてのソケットを表示
    •	-u → UDPソケットのみを表示

例:

State Recv-Q Send-Q Local Address:Port Peer Address:Port
UNCONN 0 0 192.168.1.100:123 0.0.0.0:\*

ポイント:
• UNCONN（未接続）状態のソケットが多い（UDPは接続を確立しないため）。

💡 追加の ss コマンドメモ

すべてのリスニングソケット（TCP + UDP）を表示

ss -l

    •	-l → リスニング中のポートのみを表示

TCP のみリスニング中のポートを表示

ss -lt

    •	-l → リスニング中
    •	-t → TCPのみ

UDP のみリスニング中のポートを表示

ss -lu

    •	-l → リスニング中
    •	-u → UDPのみ

特定のポートを使用しているプロセスを確認

sudo ss -tulpn

    •	-t → TCP
    •	-u → UDP
    •	-l → リスニング中
    •	-p → プロセス情報を表示
    •	-n → 数値表示

例:

State Recv-Q Send-Q Local Address:Port Peer Address:Port Process
LISTEN 0 128 0.0.0.0:22 0.0.0.0:\* users:(("sshd",pid=1234,fd=3))

ポイント:
• sshd プロセスがポート 22 を使用していることがわかる。

💡 ss コマンドのまとめ

コマンド 説明
ss -at すべての TCP ソケット（サービス名付き）
ss -atn すべての TCP ソケット（ポート番号付き）
ss -au すべての UDP ソケット
ss -l すべてのリスニングソケット
ss -lt リスニング中の TCP ソケット
ss -lu リスニング中の UDP ソケット
sudo ss -tulpn ポートを使用しているプロセスを表示

ss は netstat よりも高速なので、ネットワーク調査に便利です！ 😊

## Tracepath traceroute ping ifconfig とプライベートアドレスクラスの分類

ネットワーク診断コマンドのメモ

ネットワークのトラブルシューティングや接続確認に使用される主要なコマンド tracepath, traceroute, ping, ifconfig について簡潔にまとめました。

1. tracepath（パケットの経路を確認）

📌 概要
• 指定したホストまでのルートを調査。
• traceroute より権限が不要で手軽。
• 途中のルーターを確認できる。

📌 使い方

tracepath google.com

📌 出力例

1?: [LOCALHOST] pmtu 1500
1: 192.168.1.1 1.123ms
2: 192.168.0.1 5.456ms
3: 203.0.113.1 12.789ms
4: google.com 30.123ms

📌 ポイント
• パケットがどのルーターを通って目的地に届くか を表示。
• tracepath は ping のように ICMP（エコーリクエスト）を使用。

2. traceroute（パケットのルートを詳細に調査）

📌 概要
• ネットワークパスの詳細な経路を確認。
• 各ルーターのレスポンス時間（遅延）も測定。

📌 使い方

traceroute google.com

📌 出力例

traceroute to google.com (142.250.64.142), 30 hops max, 60 byte packets
1 192.168.1.1 (192.168.1.1) 1.123 ms
2 192.168.0.1 (192.168.0.1) 5.456 ms
3 203.0.113.1 (203.0.113.1) 12.789 ms
4 google.com (142.250.64.142) 30.123 ms

📌 ポイント
• 各ルーターのIPアドレス・ホスト名・遅延時間を確認可能。
• tracepath より詳細な情報が得られる。

3. ping（接続確認と遅延測定）

📌 概要
• ホストへの接続テストを実行。
• ICMPエコーリクエストを送信し、応答時間を測定。

📌 使い方

ping google.com

📌 出力例

PING google.com (142.250.64.142) 56(84) bytes of data.
64 bytes from 142.250.64.142: icmp_seq=1 ttl=118 time=24.3 ms
64 bytes from 142.250.64.142: icmp_seq=2 ttl=118 time=23.9 ms

📌 ポイント
• パケット損失や遅延を調査できる。
• インターネット接続の状態を確認 する際に便利。

4. ifconfig（ネットワークインターフェース情報の表示）
   📌 概要 • IPアドレスやMACアドレス、ネットワーク情報を確認 できる。 • ip a の方が推奨されるが、古い環境では ifconfig が使われる。
   📌 使い方

ifconfig

📌 出力例

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
inet 192.168.1.10 netmask 255.255.255.0 broadcast 192.168.1.255
ether 00:1a:2b:3c:4d:5e txqueuelen 1000

📌 ポイント
• inet → IPv4アドレス
• netmask → サブネットマスク
• ether → MACアドレス
• UP があればネットワーク有効

📌 インターフェースごとの情報を確認

ifconfig eth0

📌 ifconfig でIPを変更

sudo ifconfig eth0 192.168.1.50 netmask 255.255.255.0

（ただし ip addr の使用が推奨）

5. プライベートIPアドレス（LAN用IPアドレス）

プライベートIPアドレスは LAN内（ローカルネットワーク） で使用され、インターネットには直接接続できない。

📌 クラスごとの範囲

クラス IP範囲 ホスト数 用途
クラスA 10.0.0.0 - 10.255.255.255 約1677万台 大規模ネットワーク
クラスB 172.16.0.0 - 172.31.255.255 約65,000台 中規模ネットワーク
クラスC 192.168.0.0 - 192.168.255.255 約254台 家庭・小規模ネットワーク

📌 ポイント
• ルーターを介してNAT変換し、グローバルIPと通信 する。
• インターネットには直接アクセス不可。

💡 まとめ

コマンド 用途 例
tracepath パケットの経路を確認（権限不要） tracepath google.com
traceroute パケットの詳細な経路を確認 traceroute google.com
ping 接続確認・遅延測定 ping google.com
ifconfig ネットワーク設定の確認 ifconfig eth0

クラス プライベートIP範囲 用途
A 10.0.0.0 - 10.255.255.255 大規模ネットワーク
B 172.16.0.0 - 172.31.255.255 中規模ネットワーク
C 192.168.0.0 - 192.168.255.255 小規模ネットワーク

ネットワーク診断やIPアドレス設定時に tracepath, traceroute, ping, ifconfig を活用しましょう！ 😊

## 手動でのマウントに対するsystemdの挙動について、正しい説明は次のうちどれか。

手動でのマウントに対する systemd の挙動について、正しい説明はどれか？

選択肢: 1. システム起動時の自動マウント以外は systemd の監視の対象外である 2. systemd はマウントポイントを認識して監視する 3. 一定時間後に systemd がアンマウントを行う 4. systemd のマウントオプション設定にもとづき管理される

正解:

✅ 2. systemd はマウントポイントを認識して監視する

systemd は /proc/self/mountinfo を監視し、マウントポイントの状態を把握します。
手動でのマウントも systemd によって認識され、管理の対象になります。

各選択肢の解説

1. ❌ システム起動時の自動マウント以外は systemd の監視の対象外である
   • 誤り。
   systemd は /proc/mounts を監視し、手動マウントも認識するため、自動マウントだけを監視するわけではない。

2. ✅ systemd はマウントポイントを認識して監視する
   • 正しい。
   systemd は、手動マウントも含めてマウントポイントを監視する。

3. ❌ 一定時間後に systemd がアンマウントを行う
   • 誤り。
   systemd によって自動アンマウントされることは基本的にない。
   ただし、systemd.automount の設定がある場合は、一定時間使用されないとアンマウントされる（TimeoutIdleSec）。

4. ❌ systemd のマウントオプション設定にもとづき管理される
   • 誤り。
   手動マウントは、/etc/fstab や systemd のマウントユニットに依存しないため、必ずしも systemd の設定によって管理されるわけではない。

補足: systemd のマウント管理の仕組み
• systemd は、マウントポイントの状態を監視するが、手動マウントしたものを強制的に制御するわけではない。
• 自動マウント (systemd.automount) を設定すると、一定時間未使用の際にアンマウントされる場合がある。
• /etc/fstab に定義されている場合、systemd はこれをもとにマウントの管理を行う。

結論

手動マウントでも systemd はマウントポイントを認識し、監視の対象となるため、「systemd はマウントポイントを認識して監視する」 が正解！

## 「file」ファイル内でスペースが連続している場合、スペース1つに置き換えて表示させたい。適切なコマンドは次のうちどれか。(全て選択)

```sh
- tr -d [:space:] < file
- cat file | tr -s " "
- cat file | tr -b " "
- cat file | tr -d [:space:]
- tr -s [:space:] < file
```

...

### 正解:

✅ cat file | tr -s " "
✅ tr -s [:space:] < file

### 各コマンドの解説

1. tr -d [:space:] < file（❌ 不正解）
   • -d は 指定した文字を削除 するオプション。
   • [:space:] は スペース・タブ・改行を含む ため、すべての空白が削除されてしまう。

実行結果（例）

```sh
echo "Hello World " | tr -d "[:space:]"

HelloWorld
```

→ すべての空白が削除されるため不正解！

2. cat file | tr -s " "（✅ 正解）
   • -s は 連続した文字を 1 つに圧縮 するオプション。
   • " "（スペース）を指定しているので、連続するスペースを 1 つにまとめる。

実行例

```sh
echo "Hello World " | tr -s " "

Hello World
```

→ 連続するスペースが 1 つに置き換わるため正解！

3. cat file | tr -b " "（❌ 不正解）
   • -b オプションは tr には存在しないため、無効なコマンド。

→ 不正解！

4. cat file | tr -d [:space:]（❌ 不正解）
   • -d は削除するオプションなので、すべての空白（スペース・タブ・改行など）が削除される。

→ 空白を 1 つに置き換えるのではなく、完全に削除するため不正解！

5. tr -s [:space:] < file（✅ 正解）
   • -s は 連続する文字を 1 つに圧縮 する。
   • [:space:] を指定すると、スペース・タブ・改行などの空白を 1 つにまとめる。

実行例

```sh
echo "Hello World " | tr -s "[:space:]"

Hello World
```

→ 連続する空白が 1 つに置き換わるため正解！

まとめ

コマンド 正解 or 不正解 説明
tr -d [:space:] < file ❌ 不正解 空白をすべて削除してしまう
cat file | tr -s " " ✅ 正解 連続するスペースを 1 つに圧縮
cat file | tr -b " " ❌ 不正解 tr に -b オプションは存在しない
cat file | tr -d [:space:] ❌ 不正解 空白をすべて削除してしまう
tr -s [:space:] < file ✅ 正解 連続する空白（スペース・タブ・改行）を 1 つに圧縮

💡 ポイント
• tr -s は 連続する文字を 1 つにまとめる。
• -d は削除なので不適切（空白を完全に消す）。
• -b オプションは存在しないので間違い。

したがって、
✅ cat file | tr -s " "
✅ tr -s [:space:] < file
が 正解！ 🎯

## 「file」ファイルにある連続して重複した行を1行にまとめて、「newfile」ファイルに出力したい。適切なコマンドは次のうちどれか。なお、「file」ファイルはソートされている。

fmt file newfile
uniq -d file newfile
split file newfile
uniq -u file newfile
uniq file newfile

正解:

✅ uniq file newfile

各コマンドの解説

1. fmt file newfile（❌ 不正解）
   • fmt は テキストの整形（折り返し） を行うコマンドであり、重複行の削除はしない。
   • → 不適切！

2. uniq -d file newfile（❌ 不正解）
   • uniq -d は 重複している行のみを表示 するが、1つにまとめる処理ではない。
   • 例:

echo -e "A\nA\nB\nC\nC\n" | uniq -d

出力:

A
C

    •	→ 重複した行のうち1回だけを出力するため、完全な答えではない！

3. split file newfile（❌ 不正解）
   • split コマンドは ファイルを分割する コマンドであり、重複削除とは無関係。
   • → 不適切！

4. uniq -u file newfile（❌ 不正解）
   • uniq -u は 一度しか出現しない行を表示 するオプション。
   • 例:

echo -e "A\nA\nB\nC\nC\n" | uniq -u

出力:

B

    •	→ 重複行を1つにまとめるのではなく、“ユニークな行”（1回しか出現しない行）を抽出するため不適切！

5. uniq file newfile（✅ 正解）
   • uniq コマンドは 連続する重複行を1つにまとめる。
   • 例:

echo -e "A\nA\nB\nC\nC\n" | uniq

出力:

A
B
C

    •	file を処理して newfile に保存するには：

uniq file > newfile

    •	→ これが正解！

まとめ

コマンド 説明 正誤
fmt file newfile テキスト整形（折り返し）を行うだけ ❌
uniq -d file newfile 重複行のみ表示（1行にまとめない） ❌
split file newfile ファイルを分割するだけ（重複行は関係なし） ❌
uniq -u file newfile ユニークな行（1回しか出現しない行）のみ表示 ❌
uniq file newfile 連続する重複行を1つにまとめる ✅

💡 ポイント
• uniq は 隣接する重複行を1つにまとめる（ただし 事前に sort で並べ替えておく必要がある）。
• uniq file > newfile で新しいファイルに保存可能！

✅ よって、正解は uniq file newfile（または uniq file > newfile）！ 🎯

## httpd.conf」ファイルの末尾5行を表示したい。適切なコマンドは次のうちどれか。(全て選択)

tail -n 5 httpd.conf
tail -5 httpd.conf
tail -c 5 httpd.conf
tail 5 httpd.conf
tail -l 5 httpd.conf

正解:

✅ tail -n 5 httpd.conf
✅ tail -5 httpd.conf

各コマンドの解説

1. tail -n 5 httpd.conf（✅ 正解）
   • -n オプションは 表示する行数を指定 する。
   • -n 5 は 末尾から 5 行を表示。

実行例:

tail -n 5 httpd.conf

出力例:

Line 96
Line 97
Line 98
Line 99
Line 100

✅ 正解！

2. tail -5 httpd.conf（✅ 正解）
   • tail -n の -n は省略可能なので、tail -5 も tail -n 5 と同じ意味。
   • tail -5 でも末尾 5 行を表示できる。

実行例:

tail -5 httpd.conf

出力例:

Line 96
Line 97
Line 98
Line 99
Line 100

✅ 正解！

3. tail -c 5 httpd.conf（❌ 不正解）
   • -c は 文字数単位 で指定するオプション。
   • -c 5 は ファイルの末尾 5 文字のみを表示する。

実行例:

tail -c 5 httpd.conf

出力例（ファイルの内容によるが…）

f 100

❌ 行単位ではなく、“文字数単位”** なので不正解！**

4. tail 5 httpd.conf（❌ 不正解）
   • tail コマンドには、引数なしで行数を指定する機能はない。
   • tail: cannot open '5' for reading: No such file or directory のエラーになる。

❌ 不正解！

5. tail -l 5 httpd.conf（❌ 不正解）
   • tail コマンドには -l というオプションは存在しない。
   • tail: invalid option -- 'l' のエラーになる。

❌ 不正解！

まとめ

コマンド 説明 正誤
tail -n 5 httpd.conf 末尾から 5 行を表示 ✅
tail -5 httpd.conf 末尾から 5 行を表示（-n 省略可） ✅
tail -c 5 httpd.conf 末尾から 5 文字を表示（行ではない） ❌
tail 5 httpd.conf エラー（tail は直接数値を受け付けない） ❌
tail -l 5 httpd.conf エラー（-l オプションは存在しない） ❌

💡 ポイント
• tail -n 5 または tail -5 で 末尾の 5 行を取得可能！
• -c は 文字数単位 なので 行の取得には使えない。
• -l は 無効なオプション なので使用不可。

✅ よって、正解は tail -n 5 httpd.conf と tail -5 httpd.conf！ 🎯

## 「file」ファイルを行番号をつけて出力したい。適切なコマンドは次のうちどれか。なお、行番号は空行を除いた行に付けることとする。(全て選択)

num file
nl -b a file
cat -n file
nl file
cat -b file

正解:

✅ nl file
✅ cat -b file

各コマンドの解説

1. num file（❌ 不正解）
   • num というコマンドは Linux の標準コマンドには存在しない。
   • → エラーになるため不正解！

2. nl -b a file（❌ 不正解）
   • nl コマンドは行番号を付けるが、-b a は 空行も含めて行番号を振る オプション。
   • 空行を除いた行に番号をつける条件に合わないため不正解！

実行例:

echo -e "Hello\n\nWorld" | nl -b a

出力（空行にも番号がつく）:

     1  Hello

     2  World

❌ 空行にも番号がついてしまうので不適切！

3. cat -n file（❌ 不正解）
   • cat -n は 全ての行（空行を含む）に番号をつける。
   • 空行を除いた行に番号をつける条件に合わないため不正解！

実行例:

echo -e "Hello\n\nWorld" | cat -n

出力（空行にも番号がつく）:

     1  Hello
     2
     3  World

❌ 空行にも番号がついてしまうので不適切！

4. nl file（✅ 正解）
   • nl コマンドは デフォルトで空行を無視 して行番号を振る。
   • 条件に適合するので正解！

実行例:

echo -e "Hello\n\nWorld" | nl

出力（空行には番号がつかない）:

     1  Hello

     2  World

✅ 空行を除いて番号を付けるので適切！

5. cat -b file（✅ 正解）
   • cat -b は 空行を無視して行番号を振る。
   • 条件に適合するので正解！

実行例:

echo -e "Hello\n\nWorld" | cat -b

出力（空行には番号がつかない）:

     1  Hello

     2  World

✅ 空行を除いて番号を付けるので適切！

まとめ

コマンド 説明 正誤
num file num コマンドは存在しない ❌
nl -b a file 空行を含めて番号をつけるので条件不適合 ❌
cat -n file 空行にも番号をつけてしまうので条件不適合 ❌
nl file 空行を除いて番号をつけるので適合 ✅
cat -b file 空行を除いて番号をつけるので適合 ✅

💡 ポイント
• nl file → デフォルトで空行を無視して行番号を振る → ✅ 正解！
• cat -b file → 空行を除いて番号をつける → ✅ 正解！
• cat -n file → 空行にも番号をつけてしまう → ❌ 不適切！

✅ よって、正解は nl file と cat -b file！ 🎯

## 「httpd.conf」ファイルの文字(バイト)数のみを表示したい。適切なコマンドは次のうちどれか。

wc -w httpd.conf
wc httpd.conf
wc -t httpd.conf
wc -c httpd.conf
wc -l httpd.conf

正解:

✅ wc -c httpd.conf

各コマンドの解説

1. wc -w httpd.conf（❌ 不正解）
   • -w は 単語数（word count）をカウント するオプション。
   • 文字数（バイト数）ではない ので不適切。

実行例:

echo "Hello world" | wc -w

出力:

2

（“Hello” と “world” で 2 単語）

❌ 文字数ではなく単語数を数えるので不正解！

2. wc httpd.conf（❌ 不正解）
   • wc 単体では、行数・単語数・バイト数 をすべて表示する。
   • 文字数のみを表示しないので条件不適合！

実行例:

echo "Hello world" | wc

出力（3つの情報が出る）:

1 2 12

（行数: 1、単語数: 2、バイト数: 12）

❌ 文字数のみを表示しないので不正解！

3. wc -t httpd.conf（❌ 不正解）
   • -t オプションは存在しない のでエラーになる。

実行例:

wc -t httpd.conf

エラー:

wc: invalid option -- 't'

❌ -t オプションは無効なので不正解！

4. wc -c httpd.conf（✅ 正解）
   • -c は バイト数（= 文字数）を表示する オプション。
   • 指定のファイルの文字数（バイト単位）をカウントするので適切！

実行例:

echo "Hello world" | wc -c

出力:

12

（改行込みで 12 バイト）

✅ 文字数（バイト数）を取得できるので正解！

5. wc -l httpd.conf（❌ 不正解）
   • -l は 行数（line count）をカウント するオプション。
   • 文字数ではない ので不適切。

実行例:

echo -e "Hello\nworld" | wc -l

出力:

2

（改行ごとにカウントされ、2 行）

❌ 文字数をカウントしないので不正解！

まとめ

コマンド 説明 正誤
wc -w httpd.conf 単語数をカウント（文字数ではない） ❌
wc httpd.conf 行数・単語数・バイト数をすべて表示 ❌
wc -t httpd.conf -t オプションは無効 ❌
wc -c httpd.conf 文字数（バイト数）をカウント ✅
wc -l httpd.conf 行数をカウント（文字数ではない） ❌

💡 ポイント
• wc -c → バイト数（文字数）を表示 → ✅ 正解！
• wc -w → 単語数をカウント → ❌
• wc -l → 行数をカウント → ❌
• wc 単体は 行数・単語数・バイト数をまとめて表示 するので ❌

✅ よって、正解は wc -c httpd.conf！ 🎯

## Zypper コマンドでリポジトリを更新する方法

### 問題

zypper コマンドを使用して、リポジトリを更新 したい。
適切なコマンドを選択せよ。

選択肢
• zypper updaterep
• zypper list-updates
• zypper update
• zypper refresh
• zypper repos

### 正解

✅ zypper refresh

### 解説

zypper は、openSUSE や SUSE Linux Enterprise (SLE) で使用されるパッケージ管理ツールです。
リポジトリの更新（メタデータのリフレッシュ）には refresh オプションを使用します。

Zypper の主なリポジトリ関連コマンド

コマンド 説明
zypper refresh リポジトリのメタデータを更新
zypper repos 登録されているリポジトリの一覧を表示
zypper list-updates 利用可能なパッケージのアップデートを表示
zypper update パッケージの更新を実行（リポジトリの更新とは異なる）

### 各選択肢の解説

✅ zypper refresh
• リポジトリのメタデータを更新（キャッシュをリフレッシュ） するコマンド。
• パッケージリストの最新情報を取得 するため、リポジトリの更新にはこのコマンドが正しい。

❌ zypper updaterep
• このコマンドは存在しない ためエラーになる。

❌ zypper list-updates
• リポジトリの更新ではなく、利用可能なアップデート一覧を表示 するコマンド。
• 例: zypper list-updates を実行すると、アップグレード可能なパッケージが一覧表示される。
• リポジトリの更新とは無関係なので不適切！

❌ zypper update
• パッケージのアップデートを行うコマンド。
• 例えば、zypper update を実行すると、システム内の全パッケージが最新バージョンに更新される。
• リポジトリのメタデータを更新するわけではないため不適切！

❌ zypper repos
• 登録されているリポジトリの一覧を表示するコマンド。
• 例: zypper repos を実行すると、現在のリポジトリの一覧が表示される。
• リポジトリのメタデータを更新するわけではないので不適切！

### まとめ

コマンド 動作 正誤
zypper refresh リポジトリのメタデータを更新 ✅
zypper updaterep 無効なコマンド（存在しない） ❌
zypper list-updates 利用可能なアップデートを表示 ❌
zypper update パッケージの更新を実行 ❌
zypper repos 登録されているリポジトリを一覧表示 ❌

💡 ポイント
• リポジトリの更新 → zypper refresh ✅
• パッケージの一覧表示 → zypper list-updates ❌
• パッケージの更新 → zypper update ❌
• リポジトリの一覧表示 → zypper repos ❌

✅ リポジトリを更新するには zypper refresh を使う！

## ファイルのアクセス時刻のみが更新されるコマンド

### 問題

original というファイルに対して、コマンド実行後、ファイルのアクセス時刻（atime） のみが更新されるものはどれか。

選択肢
• touch original
• echo "original" > original
• ls -l original > original
• file original

### 正解

✅ file original

### 解説

Unix では、ファイルには アクセス時刻（atime）, 変更時刻（mtime）, 作成時刻（ctime） の3つのタイムスタンプがあります。

タイムスタンプ 説明
atime (access time) ファイルを読み取ったときに更新 される
mtime (modification time) ファイルの内容が変更されたときに更新 される
ctime (change time) ファイルのメタデータ（パーミッションなど）が変更されたときに更新 される

file original は、ファイルの種類を判別するコマンドですが、ファイルの内容を書き換えないため、アクセス時刻（atime）のみが更新される ことが特徴です。

各選択肢の解説

✅ file original
• file コマンドは、ファイルの種類を判別するために ファイルの内容を読み取る。
• 読み取りのみ 行われるため、アクセス時刻（atime）のみが更新 される。
• ファイルの中身は変更されない ので、変更時刻（mtime）は更新されない。

❌ touch original
• touch コマンドは、ファイルのアクセス時刻（atime）と変更時刻（mtime）を更新 する。
• touch original を実行すると、atime だけでなく mtime も更新される ため不適切。

❌ echo "original" > original
• > リダイレクトを使うと、ファイルの内容が上書きされるため、変更時刻（mtime）が更新 される。
• ファイルの変更が発生するため、atime だけが更新されるわけではない。

❌ ls -l original > original
• > で自身に上書きしようとすると、ファイルの内容が破壊されるため、変更時刻（mtime）が更新 される。
• ファイルのメタデータ（ctime）も変更される可能性がある ため、atime だけが更新されるわけではない。

### まとめ

コマンド 動作 atime のみ更新 正誤
file original ファイルを読み取るだけ ✅ ✅
touch original atime と mtime を更新 ❌ ❌
echo "original" > original ファイルの内容を変更 ❌ ❌
ls -l original > original ファイルの内容を上書き ❌ ❌

💡 ポイント
• ファイルを読み取るだけ → file original → ✅ atime のみ更新
• ファイルの時刻を変更 → touch original → ❌ atime と mtime を更新
• ファイルの内容を変更 → echo "original" > original → ❌ atime, mtime, ctime 更新
• ファイルを書き換え → ls -l original > original → ❌ atime, mtime, ctime 更新

✅ アクセス時刻（atime）だけを更新するのは file original！

## gzip形式で圧縮したアーカイブファイル「test.tar.gz」の内容を表示する方法

### 問題

gzip 形式で圧縮されたアーカイブファイル test.tar.gz の内容を表示 したい。
適切なコマンドを 2つ選択 せよ。

選択肢
• tar tjvf test.tar.gz
• tar tjf test.tar.gz
• tar ftvz test.tar.gz
• tar ftz test.tar.gz
• tar cvf test.tar.gz

### 正解

✅ tar ftvz test.tar.gz
✅ tar ftz test.tar.gz

### 解説

gzip 圧縮された tar アーカイブの内容を表示する方法

tar コマンドを使用して .tar.gz ファイルの内容を表示する際、以下のオプションを使用します。

オプション 説明
t アーカイブの内容を一覧表示する（リストモード）
f 指定したファイルを操作対象にする
z gzip 形式の圧縮を扱う
v 詳細（verbose）な情報を表示する（オプション）

したがって、t + f + z を含むコマンドが正解となります。

各選択肢の解説

✅ tar ftvz test.tar.gz
• f：ファイルを指定
• t：内容を表示
• v：詳細表示
• z：gzip 圧縮対応
→ 正解！gzip 圧縮された tar ファイルの中身を詳細に表示

✅ tar ftz test.tar.gz
• f：ファイルを指定
• t：内容を表示
• z：gzip 圧縮対応
→ 正解！gzip 圧縮された tar ファイルの中身を表示（詳細なし）

❌ tar tjvf test.tar.gz
• j オプションは bzip2 圧縮（.tar.bz2） 用のオプション
• gzip 圧縮（.tar.gz）には z を使うべき
• → 不正解！gzip ではなく bzip2 用なのでエラーになる

❌ tar tjf test.tar.gz
• j（bzip2）を使用しているため gzip 圧縮の test.tar.gz には適さない
• → 不正解！gzip ではなく bzip2 用なのでエラーになる

❌ tar cvf test.tar.gz
• c：新しいアーカイブを作成する（create）
• v：詳細表示
• f：ファイルを指定
• → 不正解！これは内容を表示するコマンドではなく、新しい test.tar.gz を作成するコマンド

### まとめ

コマンド 説明 正誤
tar ftvz test.tar.gz gzip 圧縮された tar ファイルの詳細な内容を表示 ✅
tar ftz test.tar.gz gzip 圧縮された tar ファイルの内容を表示 ✅
tar tjvf test.tar.gz bzip2 圧縮された tar ファイルの詳細な内容を表示（gzip では使えない） ❌
tar tjf test.tar.gz bzip2 圧縮された tar ファイルの内容を表示（gzip では使えない） ❌
tar cvf test.tar.gz アーカイブを作成する（内容表示ではない） ❌

💡 ポイント
• gzip 圧縮された tar の内容を表示する → tar ftvz または tar ftz
• bzip2 圧縮された tar の内容を表示する → tar tjvf または tar tjf
• アーカイブの作成は c（create）オプション
• リスト表示（t）は内容確認専用、解凍はしない

✅ gzip 圧縮された tar ファイルの内容を表示するには tar ftvz test.tar.gz または tar ftz test.tar.gz！

## 「configure」ファイルをbzip2形式で圧縮する方法

### 問題

configure ファイルを bzip2形式で圧縮 したい。
適切なコマンドを選択せよ。

選択肢
• bzip2 configure
• bzip2 -d configure
• gzip configure
• gzip -d configure
• bunzip2 configure

### 正解

✅ bzip2 configure

### 解説

bzip2 は、bzip2形式（.bz2） でファイルを圧縮するコマンドです。
bzip2 configure を実行すると、configure ファイルが configure.bz2 に圧縮されます。

コマンド 説明
bzip2 bzip2 形式で圧縮する
bunzip2 bzip2 形式の圧縮を解除する
gzip gzip 形式で圧縮する（bzip2とは異なる）
gunzip gzip 形式の圧縮を解除する

各選択肢の解説

✅ bzip2 configure
• configure を configure.bz2 に圧縮する
• 正解！bzip2 形式での圧縮コマンド

❌ bzip2 -d configure
• -d オプションは圧縮解除（解凍）のためのもの
• 圧縮ではなく、展開するときに使うコマンドなので不適切

❌ gzip configure
• gzip 形式（.gz）で圧縮するコマンド
• bzip2（.bz2）形式ではないため不適切

❌ gzip -d configure
• gzip 形式の圧縮を解除する（解凍）コマンド
• 圧縮ではなく、展開するときに使うコマンドなので不適切

❌ bunzip2 configure
• bzip2 形式の圧縮を解除するコマンド
• 圧縮ではなく、解凍するためのコマンドなので不適切

### まとめ

コマンド 動作 正誤
bzip2 configure bzip2 形式（.bz2）で圧縮する ✅
bzip2 -d configure bzip2 形式（.bz2）を解凍する ❌
gzip configure gzip 形式（.gz）で圧縮する ❌
gzip -d configure gzip 形式（.gz）を解凍する ❌
bunzip2 configure bzip2 形式（.bz2）を解凍する ❌

💡 ポイント
• bzip2 形式で圧縮 → bzip2 ファイル名
• bzip2 形式の解凍 → bzip2 -d ファイル名 または bunzip2 ファイル名
• gzip 形式で圧縮 → gzip ファイル名（bzip2 とは異なる）
• gzip 形式の解凍 → gzip -d ファイル名 または gunzip ファイル名

✅ bzip2形式で「configure」を圧縮するには bzip2 configure を使う！

## アクセス権が700の「dir」ディレクトリを作成する方法

### 問題

アクセス権が 700 の dir ディレクトリを作成したい。
適切なコマンドを選択せよ。

選択肢
• mkdir 700 dir
• mkdir dir 700
• mkdir -p 700 dir
• mkdir -m 700 dir
• mkdir dir -p 700

### 正解

✅ mkdir -m 700 dir

解説

mkdir コマンドは 新しいディレクトリを作成 するために使用されます。
デフォルトでは umask の設定に従ってパーミッションが決定 されますが、-m オプションを使用すると、作成時に明示的にアクセス権を指定 できます。

オプション 説明
-m mode 作成するディレクトリのパーミッションを指定する
-p 親ディレクトリがない場合に自動作成する

-m 700 を指定すると、作成される dir ディレクトリのアクセス権が rwx------（オーナーのみアクセス可能） になります。

### 各選択肢の解説

✅ mkdir -m 700 dir
• -m 700 オプションにより、作成時にパーミッションを700に設定
• 正解！意図したアクセス権を持つディレクトリを作成できる

❌ mkdir 700 dir
• mkdir は オプションなしで直接パーミッションを指定できない
• 700 がディレクトリ名として解釈される
• → 不適切！構文エラーになる

❌ mkdir dir 700
• 700 が ディレクトリ名として扱われてしまう
• パーミッションとして適用されない
• → 不適切！意図した動作にならない

❌ mkdir -p 700 dir
• -p は 親ディレクトリが存在しない場合に自動作成するオプション
• 700 が ディレクトリ名として扱われる
• → 不適切！パーミッションは指定できていない

❌ mkdir dir -p 700
• -p はディレクトリ作成時のオプションだが、700 の位置が誤っている
• 700 が ディレクトリ名として解釈される
• → 不適切！構文エラーになる

### まとめ

コマンド 動作 正誤
mkdir -m 700 dir 700 のパーミッションで dir を作成 ✅
mkdir 700 dir 構文エラー（700 がディレクトリ名と解釈される） ❌
mkdir dir 700 700 がディレクトリ名として扱われる ❌
mkdir -p 700 dir 700 がディレクトリ名として扱われる ❌
mkdir dir -p 700 700 がディレクトリ名として扱われる（構文エラー） ❌

💡 ポイント
• ディレクトリ作成時にアクセス権を指定 → mkdir -m パーミッション ディレクトリ名
• -m オプションを使うと、作成時にパーミッションを設定できる
• 親ディレクトリを作成する場合は -p を併用可能（例：mkdir -m 700 -p /path/to/dir）

✅ アクセス権が700の「dir」ディレクトリを作成するには mkdir -m 700 dir！

##「dir」ディレクトリ内の全てのファイルをgzip形式で圧縮する方法

### 問題

dir ディレクトリ内の すべてのファイルを個別にgzip形式で圧縮 したい。
適切なコマンドを選択せよ。

選択肢
• gzip -p dir
• gzip -c dir
• gzip -r dir
• gzip dir
• gzip -d dir

### 正解

✅ gzip -r dir

### 解説

gzip コマンドは ファイルを圧縮する コマンドですが、通常は 単一ファイル を対象とします。
ディレクトリ内のすべてのファイルを圧縮するには、-r（再帰的）オプション を使用します。

オプション 説明
-r ディレクトリ内のすべてのファイルを再帰的に圧縮
-c 標準出力に圧縮データを出力（元のファイルは変更しない）
-d 圧縮ファイルを解凍する（gzip → 元ファイルに戻す）

したがって、ディレクトリ内のファイルを一括で圧縮するには gzip -r dir を使用 します。

各選択肢の解説

✅ gzip -r dir
• ディレクトリ内のすべてのファイルを圧縮（再帰的に処理）
• dir 内の 各ファイル が \*.gz 形式に圧縮される
• 正解！この方法で全ファイルを圧縮できる

❌ gzip -p dir
• gzip に -p オプションは存在しない
• 不適切！無効なオプション

❌ gzip -c dir
• -c は 圧縮データを標準出力に送るオプション であり、ファイルの圧縮には使えない
• 不適切！ディレクトリ全体の圧縮はできない

❌ gzip dir
• gzip は ディレクトリを直接圧縮できない
• 不適切！gzip は単体のファイルしか扱えない

❌ gzip -d dir
• -d は 解凍（展開）オプション
• 不適切！圧縮ではなく解凍するコマンドなので誤り

### まとめ

コマンド 動作 正誤
gzip -r dir ディレクトリ内の全ファイルを個別にgzip圧縮 ✅
gzip -p dir 無効なオプション（エラー） ❌
gzip -c dir 標準出力に圧縮データを出力（ファイルを直接圧縮しない） ❌
gzip dir ディレクトリは圧縮できない（エラー） ❌
gzip -d dir 解凍するコマンドなので不適切 ❌

💡 ポイント
• ディレクトリ内のすべてのファイルを圧縮するには gzip -r ディレクトリ名
• gzip はディレクトリを直接圧縮できない（ファイルのみ対応）
• 解凍（展開）する場合は gzip -d ファイル名.gz または gunzip ファイル名.gz を使用

✅ 「dir」ディレクトリ内のすべてのファイルをgzip形式で圧縮するには gzip -r dir！

## ファイルやデバイス間でのコピーができるコマンド

### 問題

ファイルからデバイス、デバイスからファイル、またデバイス間でのコピー を行うことができるコマンドは次のうちどれか。

選択肢
• cpio
• bzip2
• tar
• gzip
• dd

### 正解

✅ dd

### 解説

dd コマンドは、ファイルやデバイス間のデータを低レベルでコピーするためのコマンド です。
通常のファイルコピーだけでなく、ディスクやパーティション、ブートローダー、ISOイメージの作成などにも利用 できます。

dd コマンドの基本構文

dd if=<入力ファイル> of=<出力ファイル> bs=<ブロックサイズ> count=<コピーするブロック数>

オプション 説明
if= 入力ファイル（またはデバイス）を指定
of= 出力ファイル（またはデバイス）を指定
bs= ブロックサイズ（データ転送単位）を指定
count= コピーするブロック数を指定
conv= データ変換（例: noerror, sync など）

### 各選択肢の解説

✅ dd
• ファイル、デバイス、ディスクイメージなどのコピーが可能
• 例1: HDDのバックアップを作成

dd if=/dev/sda of=/backup/hdd.img bs=4M

    •	例2: ISOイメージをUSBに書き込む

dd if=ubuntu.iso of=/dev/sdb bs=4M

    •	正解！ファイルやデバイス間のコピーが可能

❌ cpio
• cpio は アーカイブを作成・展開するコマンド
• 主にバックアップ用途で使用され、デバイス間のコピーはできない
• → 不適切！ファイルのコピーには向かない

❌ bzip2
• bzip2 は ファイルを圧縮・解凍するコマンド
• ファイルのコピーやデバイス間の転送はできない
• → 不適切！圧縮・解凍専用

❌ tar
• tar は 複数のファイルをまとめてアーカイブするコマンド
• ファイルのコピーやデバイス間の転送はできない
• → 不適切！アーカイブ作成・展開専用

❌ gzip
• gzip は ファイルを圧縮するコマンド
• ファイルのコピーやデバイス間の転送はできない
• → 不適切！圧縮専用

### まとめ

コマンド 主な用途 デバイス間コピー 正誤
dd ファイルやデバイス間のコピー ✅ ✅
cpio アーカイブ作成・展開 ❌ ❌
bzip2 圧縮・解凍 ❌ ❌
tar アーカイブ作成・展開 ❌ ❌
gzip 圧縮・解凍 ❌ ❌

💡 ポイント
• ファイルやデバイスのコピー → dd if=<入力> of=<出力>
• ファイルの圧縮・解凍 → gzip / bzip2
• アーカイブ作成・展開 → tar / cpio
• HDD/USB/ISO のバックアップや転送にも dd が使われる

✅ ファイルからデバイス、デバイスからファイル、デバイス間のコピーには dd を使う！

## cpio形式のアーカイブ「backup.cpio」からファイルを展開する方法

### 問題

backup.cpio という cpio形式のアーカイブ から ファイルを展開（復元） したい。
適切なコマンドを選択せよ。

選択肢

    •	cpio -o < backup.cpio
    •	cpio backup.cpio
    •	cpio -i < backup.cpio
    •	cpio -o backup.cpio
    •	cpio -i backup.cpio

### 正解

```sh
✅ cpio -i < backup.cpio
```

### 解説

cpio は、ファイルのアーカイブと展開を行うためのコマンド です。
cpio -i を使うと cpio 形式のアーカイブからファイルを展開（復元） できます。

cpio の基本オプション

オプション 説明
-o アーカイブを作成（オリジナルの保存）
-i アーカイブを展開（復元）
-p ファイルを別のディレクトリへコピー（パススルー）

```sh
したがって、ファイルを展開するには -i オプションを使用し、backup.cpio を入力として渡す必要がある ため、
cpio -i < backup.cpio が正解となります。
```

各選択肢の解説

```
✅ cpio -i < backup.cpio
	•	-i → アーカイブを展開
	•	< backup.cpio → アーカイブを標準入力として読み込む
	•	→ 正解！cpio 形式のアーカイブからファイルを展開する

❌ cpio -o < backup.cpio
	•	-o は アーカイブの作成（出力）用のオプション
	•	アーカイブの展開（復元）には使えない
	•	→ 不適切！誤ったオプション

❌ cpio backup.cpio
	•	cpio は 直接ファイル名を指定して展開できない
	•	標準入力を利用する必要がある
	•	→ 不適切！構文エラーになる

❌ cpio -o backup.cpio
	•	-o は アーカイブの作成 に使うオプション
	•	展開（復元）には -i を使うべき
	•	→ 不適切！誤ったオプション

❌ cpio -i backup.cpio
	•	cpio -i を使っているので一見正しそうだが、cpio は 標準入力からアーカイブを展開するため、< を使ってデータを渡す必要がある
	•	backup.cpio を直接指定しても動作しない
	•	→ 不適切！入力方法が間違っている
```

### まとめ

```
コマンド	動作	正誤
cpio -i < backup.cpio	cpio アーカイブを展開（復元）	✅
cpio -o < backup.cpio	アーカイブを作成（復元ではない）	❌
cpio backup.cpio	誤った構文（標準入力を使用しないと動作しない）	❌
cpio -o backup.cpio	アーカイブを作成（復元ではない）	❌
cpio -i backup.cpio	誤った構文（標準入力が必要）	❌

💡 ポイント
	•	アーカイブを作成する → find . | cpio -o > archive.cpio
	•	アーカイブを展開する → cpio -i < archive.cpio
	•	cpio は通常、標準入力・標準出力を使用する（直接ファイルを指定しない）
	•	バックアップ用途や古いUNIX系システムで利用されることが多い

✅ cpio形式のアーカイブ「backup.cpio」からファイルを展開するには cpio -i < backup.cpio！
```

##「configure」ファイルをxz形式で「configure.xz」に圧縮し、元ファイルを残す方法

### 問題

configure ファイルを xz形式（.xz）で圧縮 し、configure.xz というファイルを作成したい。
また、圧縮前の元ファイルも削除せずに残したい。
適切なコマンドを選択せよ。

選択肢
• xz -k configure
• xz -d configure configure.xz
• xz -l configure configure.xz
• xz configure configure.xz
• xz -d configure > configure.xz

### 正解

✅ xz -k configure

### 解説

xz コマンドは、LZMAベースの圧縮を行うツール で、gzip や bzip2 と同様に、ファイルを圧縮・解凍できます。
デフォルトでは、xz でファイルを圧縮すると 元ファイルが削除される ため、元ファイルを残すには -k（keep）オプションを使用 します。

オプション 説明
-k 元のファイルを削除せずに保持する
-d xz圧縮されたファイルを解凍する（decompress）
-l xzアーカイブの情報を表示する（リスト表示）

したがって、圧縮後に元ファイルを残すには xz -k configure を使用 します。

各選択肢の解説

✅ xz -k configure
• -k オプションにより 元ファイルを削除せずに圧縮
• configure → configure.xz が作成され、configure もそのまま残る
• → 正解！期待通りの動作をする

❌ xz -d configure configure.xz
• -d は 解凍（展開）オプション であり、圧縮には使用しない
• → 不適切！圧縮ではなく解凍のコマンドになっている

❌ xz -l configure configure.xz
• -l は xzファイルの情報をリスト表示するオプション
• 圧縮は行われない
• → 不適切！ファイルを圧縮できない

❌ xz configure configure.xz
• xz コマンドは 出力ファイル名を直接指定できない
• xz configure を実行すると、configure が configure.xz に圧縮されるが、元ファイルは削除される
• → 不適切！元ファイルが削除される

❌ xz -d configure > configure.xz
• -d は 解凍（展開）オプション
• 圧縮ではなく解凍してしまう
• → 不適切！圧縮ではなく解凍になっている

### まとめ

コマンド 動作 元ファイル保持 正誤
xz -k configure xz形式で圧縮し、元ファイルを残す ✅ ✅
xz -d configure configure.xz 解凍する（圧縮ではない） - ❌
xz -l configure configure.xz xzファイルの情報を表示する（圧縮ではない） - ❌
xz configure configure.xz 圧縮するが元ファイルが削除される ❌ ❌
xz -d configure > configure.xz 解凍する（圧縮ではない） - ❌

💡 ポイント
• xz ファイル名 で圧縮するが、元ファイルは削除される
• xz -k ファイル名 で圧縮しつつ、元ファイルを保持
• 解凍する場合は xz -d ファイル名.xz または unxz ファイル名.xz
• -l は xz ファイルの情報を表示するオプションであり、圧縮には使えない

✅ 「configure」ファイルをxz形式で「configure.xz」に圧縮し、元ファイルを残すには xz -k configure！

ファイルやデバイス間でのコピーができるコマンド

問題

ファイルからデバイス、デバイスからファイル、またデバイス間でのコピー を行うことができるコマンドは次のうちどれか。

選択肢
• tar
• gzip
• dd
• cpio
• bzip2

正解

✅ dd

解説

dd コマンドは、ファイルやデバイス間のデータを低レベルでコピーするためのコマンド です。
通常のファイルコピーだけでなく、ディスクやパーティション、ブートローダー、ISOイメージの作成などにも利用 できます。

dd コマンドの基本構文

dd if=<入力ファイル> of=<出力ファイル> bs=<ブロックサイズ> count=<コピーするブロック数>

オプション 説明
if= 入力ファイル（またはデバイス）を指定
of= 出力ファイル（またはデバイス）を指定
bs= ブロックサイズ（データ転送単位）を指定
count= コピーするブロック数を指定
conv= データ変換（例: noerror, sync など）

各選択肢の解説

✅ dd
• ファイル、デバイス、ディスクイメージなどのコピーが可能
• 例1: HDDのバックアップを作成

dd if=/dev/sda of=/backup/hdd.img bs=4M

    •	例2: ISOイメージをUSBに書き込む

dd if=ubuntu.iso of=/dev/sdb bs=4M

    •	正解！ファイルやデバイス間のコピーが可能

❌ tar
• tar は 複数のファイルをまとめてアーカイブするコマンド
• ファイルのコピーやデバイス間の転送はできない
• → 不適切！アーカイブ作成・展開専用

❌ gzip
• gzip は ファイルを圧縮するコマンド
• ファイルのコピーやデバイス間の転送はできない
• → 不適切！圧縮専用

❌ cpio
• cpio は アーカイブを作成・展開するコマンド
• 主にバックアップ用途で使用され、デバイス間のコピーはできない
• → 不適切！ファイルのコピーには向かない

❌ bzip2
• bzip2 は ファイルを圧縮・解凍するコマンド
• ファイルのコピーやデバイス間の転送はできない
• → 不適切！圧縮・解凍専用

まとめ

コマンド 主な用途 デバイス間コピー 正誤
dd ファイルやデバイス間のコピー ✅ ✅
tar アーカイブ作成・展開 ❌ ❌
gzip 圧縮・解凍 ❌ ❌
cpio アーカイブ作成・展開 ❌ ❌
bzip2 圧縮・解凍 ❌ ❌

💡 ポイント
• ファイルやデバイスのコピー → dd if=<入力> of=<出力>
• ファイルの圧縮・解凍 → gzip / bzip2
• アーカイブ作成・展開 → tar / cpio
• HDD/USB/ISO のバックアップや転送にも dd が使われる

✅ ファイルからデバイス、デバイスからファイル、デバイス間のコピーには dd を使う！
