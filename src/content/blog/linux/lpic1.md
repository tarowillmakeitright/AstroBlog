---
author: Taro Gray
pubDatetime: 2025-01-30T08:00:00.000Z
title: tmuxの基本：ターミナルのプロになるためのガイド
postSlug: linux-tmux
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
description: Lpic1で疑問に思ったこと。後から見返す復習用。
---

## Table of contents

## mkfs でパーティションをして、mkswapでは何をする？

以下のように役割が異なります：

1. mkfs（Make File System）
   • 目的: ファイルシステムを作成する。
   • 使用する場面: パーティションにデータを保存可能にするため、指定したファイルシステム（例: ext4, xfs）を作成する。
   • 例:

mkfs.ext4 /dev/sda1

上記コマンドで、/dev/sda1 パーティションに ext4 ファイルシステムを作成します。

2. mkswap（Make Swap Area）
   • 目的: パーティションをスワップ領域として設定する。
   • スワップ領域とは: メモリ不足時にデータを一時的に保存する仮想メモリ領域。
   • 使用する場面: メモリが足りなくなった際のバックアップ用にスワップ領域を設定したい場合。
   • 例:

mkswap /dev/sda2

上記コマンドで、/dev/sda2 パーティションをスワップ領域として準備します。

3. 補足: swapon
   • スワップ領域を有効化するには、swapon コマンドを使います。
   • 例:

swapon /dev/sda2

結論
• mkfs は通常のファイル保存用のファイルシステムを作成。
• mkswap はスワップ領域を作成し、仮想メモリとして使用可能にする。

## Fsck とは何の略

fsck は File System Consistency Check の略です。

概要
• 目的: ファイルシステムの整合性をチェックし、必要に応じて修復を行う。
• 使用する場面: システムクラッシュや不意のシャットダウン後、ファイルシステムにエラーが発生した可能性がある場合に使用されます。

基本コマンド例

fsck /dev/sda1

上記コマンドで、/dev/sda1 のファイルシステムをチェックします。

主要オプション
• -a または --auto: 自動修復を試みる（非推奨の場合あり）。
• -y: 全ての修復確認に「Yes」と応答する。
• -n: 修復せずに問題箇所だけを報告する。

注意点
• ファイルシステムがマウントされている状態で fsck を実行すると、データの破損を招く可能性があります。そのため、通常はアンマウント状態で実行することが推奨されます。

関連コマンド
• e2fsck: ext系（ext2, ext3, ext4）ファイルシステム用のfsck。
• xfs_repair: XFSファイルシステム用の修復ツール。

fsck は、LinuxやUnixベースのシステムで重要なツールとして、ファイルシステムの問題を防ぐために定期的に使用されます。

## Mountは、パーティションを作る認識で合ってる

いいえ、mount の役割はパーティションを「作る」ことではありません。

mount の役割
• 目的: 作成済みのパーティションやデバイス（例: ハードディスク、USBメモリ）を、システムのファイルシステムとして利用可能にする。
• 具体的には: ファイルシステムをディレクトリに関連付けて、そのデータにアクセス可能な状態にする。

パーティション作成とマウントの違い 1. パーティション作成:
パーティションを作成する作業には、以下のコマンドが必要です:
• fdisk または parted: パーティションを作成・編集。
• mkfs: ファイルシステムを作成（フォーマット）。2. マウント（mount）:
作成済みのパーティションを利用可能にする作業。
• 例:

mount /dev/sda1 /mnt

上記コマンドでは、/dev/sda1 パーティションを /mnt ディレクトリにマウントします。

mount コマンドの例 1. 外部ドライブのマウント:

mount /dev/sdb1 /media/usb

    2.	既存のマウント状態を確認:

mount

    3.	特定のパーティションだけを確認:

lsblk

補足
• アンマウント（umount）: 使用が終わったデバイスをアンマウントして安全に取り外す。

umount /dev/sda1

結論

mount はパーティションを「作る」コマンドではなく、既に作成されたパーティションをシステムに接続して使えるようにするコマンドです。

## lddはどのような時に使用するか

ldd コマンドは、Linux システムで 実行可能ファイルや共有ライブラリが依存している共有オブジェクトファイル（動的ライブラリ）を表示するため に使用します。

ldd の用途 1. 依存ライブラリの確認
• 実行ファイルがどの共有ライブラリに依存しているかを確認します。
• これにより、必要なライブラリがシステムに存在するかどうかを判断できます。
使用例:

ldd /usr/bin/ls

出力例:

linux-vdso.so.1 => (0x00007fffa65d7000)
libselinux.so.1 => /lib64/libselinux.so.1 (0x00007f8b34c0d000)
libc.so.6 => /lib64/libc.so.6 (0x00007f8b3486f000)
/lib64/ld-linux-x86-64.so.2 (0x00007f8b34e32000)

説明:
• 実行ファイル /usr/bin/ls が libselinux.so.1 や libc.so.6 などに依存していることがわかります。

    2.	ライブラリの不足（not found の確認）
    •	実行ファイルが必要とするライブラリがシステムに存在しない場合に、not found という出力が表示されます。

例:

ldd /opt/nvim-linux64/bin/nvim

出力例（ライブラリが見つからない場合）:

libncursesw.so.6 => not found
libm.so.6 => /lib64/libm.so.6 (0x00007f92f15e9000)

対処法:
• not found がある場合、必要なライブラリをインストールする必要があります。

sudo apt install libncursesw6

    3.	ライブラリのパス確認
    •	システムにあるどのライブラリを実行ファイルが参照しているかを確認できます。

例:

ldd /usr/bin/grep

出力に表示されるパス（例: /lib64/libc.so.6）が、現在のシステム上の実際のライブラリです。

ldd の実行時の注意
• セキュリティ: 信頼できないバイナリに対して ldd を実行すると、バイナリ内のコードが実行される可能性があります。これは安全上のリスクです。
• 対策: ldd の代わりに以下のように安全に使用します。

objdump -p /path/to/binary | grep NEEDED

使用例まとめ1. 依存関係の確認:

ldd /path/to/binary

    2.	ライブラリ不足の確認:

ldd /path/to/binary | grep "not found"

    3.	ライブラリパスの確認:

ldd /path/to/binary

結論

ldd は実行ファイルや共有ライブラリが必要とする依存関係を確認するための重要なツールです。ライブラリが不足している場合や、正しくリンクされているかを確認する際に使用します。

## Yum gruouplistはどのような時

yum grouplist コマンドは、Red Hat 系ディストリビューション（RHEL、CentOS、Fedora） で ソフトウェアのグループ一覧 を表示する際に使用します。グループ単位でパッケージをインストール、確認、管理するために利用されます。

yum grouplist の用途 1. インストール可能なパッケージグループの確認
• システムにインストールできるソフトウェアのグループを一覧表示します。
• グループは複数の関連するパッケージをまとめたものです。
• 例: “Development Tools”, “Web Server”, “Desktop Environment” など。
使用例:

yum grouplist

出力例:

Available Environment Groups:
Minimal Install
Compute Node
Infrastructure Server
File and Print Server
MATE Desktop
Available Groups:
Development Tools
Console Internet Tools
Graphical Administration Tools
Installed Groups:
Base
Web Server

    •	Available Environment Groups: 環境単位で提供される大きなセット。
    •	Available Groups: 個別のソフトウェアグループ（小さめなグループ）。
    •	Installed Groups: 既にインストールされているグループ。

    2.	特定のグループをインストールする前の確認
    •	必要なパッケージ群をインストールする前に、どのグループが存在するかを確認できます。
    3.	システム構成の確認
    •	システムにインストールされているパッケージグループを確認します。

yum grouplist と関連コマンド

1. グループのインストール

インストールするグループを指定する場合は groupinstall を使用します。

例: Development Tools グループをインストール

yum groupinstall "Development Tools"

2. グループの削除

インストール済みのグループを削除する場合は groupremove を使用します。

例: Development Tools グループを削除

yum groupremove "Development Tools"

3. グループ内のパッケージ確認

特定のグループ内に含まれているパッケージ一覧を確認するには groupinfo を使用します。

例: Development Tools グループの詳細確認

yum groupinfo "Development Tools"

実際の使用シナリオ
• 新しいサーバー構築時: 必要なソフトウェアグループをインストール（例: Development Tools, Web Server）。
• デスクトップ環境の追加: CLI 環境にデスクトップ環境（GNOME, MATE Desktop など）を追加する際。
• パッケージの管理: どのグループがインストールされているかを確認し、不要なものを削除。

まとめ
• yum grouplist は、利用可能なパッケージグループやインストール済みのグループを一覧表示するコマンドです。
• 関連コマンド: groupinstall（インストール）、groupremove（削除）、groupinfo（詳細表示）。
• 主な用途: ソフトウェアの一括管理やインフラ構築時のパッケージ管理に使用します。

## Ssh を使えば、二つのパソコンから一つの環境を見れるよね

はい、SSH (Secure Shell) を使えば、複数のパソコンから同じリモート環境にアクセスすることが可能です。

SSH の基本的な仕組み
• SSH は 暗号化通信 を使用して、リモートのサーバーやPCに安全に接続するプロトコルです。
• 同じリモートマシンに複数のユーザーや異なる端末から同時に接続することができます。

複数のPCから同じ環境を見る方法

1. 複数の SSH 接続を使う場合
   • 複数の端末 から 同じユーザーアカウント で SSH 接続すれば、同じ環境（ホームディレクトリ、設定）にアクセスできます。
   例:
   PC1 と PC2 から同じサーバーに SSH で接続:

ssh user@remote-server

    •	PC1 でも PC2 でも user アカウントのシェルを開き、ファイルやコマンドを共有できます。

2. 同じセッションを共有する場合（tmux や screen の利用）
   • SSH で同じセッションを共有したい場合は、tmux や screen などのターミナルマルチプレクサを利用します。
   手順: tmux を使用する場合 1. リモート環境に SSH で接続:

ssh user@remote-server

    2.	tmux セッションを開始:

tmux new -s shared-session

    3.	別の端末から同じセッションに接続:
    •	別の PC から SSH 接続した後、以下を実行:

tmux attach -t shared-session

これで、複数の端末から 同じ画面 を見ることができ、コマンド入力や操作がリアルタイムで共有されます。
特徴:
• 同時編集: 複数人が同じセッションでコマンド入力や編集ができる。
• セッション保持: SSH が切断されてもセッションを再接続できる。

3. X11 転送を使う場合（GUI アプリ共有）
   • SSH の X11 転送 機能を使うと、リモート環境の GUI アプリケーションをローカルの画面に表示できます。
   例:

ssh -X user@remote-server

    •	-X オプション: X11 転送を有効化。
    •	GUI アプリケーションを起動:

xeyes # GUI アプリの例

注意: これは画面共有ではなく、リモートアプリケーションの GUI を転送して表示する機能です。

まとめ
• SSH 単体: 複数の端末から同じリモート環境に接続可能。
• tmux や screen: 同じセッション（画面）をリアルタイムで共有する場合に最適。
• X11 転送: GUI アプリケーションを転送して表示する場合に使用。

複数の端末やユーザーが SSH を使って同一環境を操作する場合は、tmux や screen を併用すると便利です。

## サーバの設定ってどうすれば良いんだろう？

### **1.1 システムの初期設定**

#### **1. パッケージの更新**

最新のセキュリティパッチやソフトウェア更新を適用します。

```bash
sudo yum update -y

2. ホスト名の設定

sudo hostnamectl set-hostname my-server

3. タイムゾーンの設定

sudo timedatectl set-timezone Asia/Tokyo

4. NTP（時刻同期）の設定

chronyd を使用してシステム時刻を同期します。

sudo yum install -y chrony
sudo systemctl enable --now chronyd

1.2 ユーザーと権限の設定

1. 管理ユーザーの追加

sudo useradd -m admin
sudo passwd admin

2. sudo 権限を付与

sudo usermod -aG wheel admin

3. root ユーザーの SSH ログイン禁止

/etc/ssh/sshd_config を編集して以下を設定:

PermitRootLogin no

SSH サービスを再起動

sudo systemctl restart sshd

1.3 ファイアウォールの設定

CentOS では firewalld が標準のファイアウォールです。

1. firewalld を有効化

sudo systemctl enable --now firewalld

2. サービスの許可（SSH, HTTP）

sudo firewall-cmd --permanent --add-service=ssh
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload

3. 設定確認

sudo firewall-cmd --list-all

2. SSH サーバーの設定

1. SSHポート変更

/etc/ssh/sshd_config を編集し、デフォルトの 22 を 2222 に変更:

Port 2222

2. SSH サービスを再起動

sudo systemctl restart sshd

3. ファイアウォールに新ポートを許可

sudo firewall-cmd --permanent --add-port=2222/tcp
sudo firewall-cmd --reload

3. Web サーバーの設定（Apache の例）

1. Apache のインストール

sudo yum install -y httpd

2. Apache の起動と自動起動設定

sudo systemctl enable --now httpd

3. ファイアウォールに HTTP/HTTPS を許可

sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --permanent --add-service=https
sudo firewall-cmd --reload

4. 動作確認

ブラウザで http://サーバーIP にアクセス。

4. データベースサーバーの設定（MariaDB の例）

1. MariaDB のインストール

sudo yum install -y mariadb-server

2. MariaDB の起動と自動起動設定

sudo systemctl enable --now mariadb

3. 初期設定

sudo mysql_secure_installation

4. MySQL シェルに接続

mysql -u root -p

5. セキュリティの強化

1. SELinux の確認

SELinux を有効化し、適切に設定します。

getenforce
sudo setenforce 1  # Enforcing モードに設定

2. Fail2ban の導入（SSH攻撃対策）

sudo yum install -y epel-release
sudo yum install -y fail2ban
sudo systemctl enable --now fail2ban

3. ログ監視ツールの導入

logwatch をインストールしてログを監視。

sudo yum install -y logwatch

6. 最終確認

1. サービスの状態確認

sudo systemctl status sshd
sudo systemctl status httpd
sudo systemctl status mariadb

2. ネットワーク設定の確認

ip a

3. ポート確認

sudo ss -tuln

まとめ
	1.	システムの初期設定: ユーザー作成、権限管理、ファイアウォール、SSH 設定。
	2.	Web サーバーの構築: Apache（または Nginx）をインストールし、公開設定。
	3.	データベースサーバーの導入: MariaDB（または MySQL）をセットアップ。
	4.	セキュリティ対策: SELinux、Fail2ban、ファイアウォールの強化。

CentOS は安定したサーバー OS なので、必要なサービスやセキュリティ設定を行えば、安全で強固な環境を構築できます。
適切な管理を行い、安全な運用を心がけましょう！

## docker ps  docker ps -a の違いは

docker ps と docker ps -a の違いは、表示される コンテナの状態 にあります。

1. docker ps
	•	意味: 稼働中のコンテナのみ を表示します。
	•	表示されるコンテナ: 現在 running（実行中） のコンテナ。
	•	使用例:

docker ps


	•	出力例:

CONTAINER ID   IMAGE          COMMAND       CREATED        STATUS       PORTS                     NAMES
1a2b3c4d5e6f   nginx:latest   "nginx -g…"   10 minutes ago Up 10 mins   0.0.0.0:80->80/tcp        my_nginx

	•	STATUS: Up で実行中の状態。

2. docker ps -a
	•	意味: すべてのコンテナ を表示します。
	•	表示されるコンテナ:
	•	running（実行中）
	•	exited（停止済み）
	•	created（作成のみ） など、すべての状態のコンテナが表示されます。
	•	使用例:

docker ps -a


	•	出力例:

CONTAINER ID   IMAGE          COMMAND       CREATED         STATUS                     PORTS                     NAMES
1a2b3c4d5e6f   nginx:latest   "nginx -g…"   10 minutes ago  Up 10 mins                 0.0.0.0:80->80/tcp        my_nginx
2b3c4d5e6f7g   ubuntu:latest  "/bin/bash"   2 hours ago     Exited (0) 1 hour ago      -                         my_ubuntu
3c4d5e6f7g8h   httpd:latest   "httpd-fore…" 5 hours ago     Created                    -                         my_httpd

	•	STATUS:
	•	Up: 実行中。
	•	Exited: 停止済み。
	•	Created: コンテナが作成されただけで未実行。

まとめ

コマンド	表示内容
docker ps	実行中 (running) のコンテナのみ。
docker ps -a	すべての状態 のコンテナを表示（実行中、停止、作成済みなど）。

補足: よく使うオプション
	•	--filter: 状態や条件を指定してフィルタリングできます。

docker ps -a --filter "status=exited"

	•	status=exited: 停止済みコンテナのみ表示。
	•	status=running: 実行中コンテナのみ表示。

	•	--format: 出力フォーマットをカスタマイズ。

docker ps --format "{{.ID}}: {{.Status}}"



これで docker ps と docker ps -a の違いが明確になります！🚀

## ハードリンくと、コピーの違いは

ハードリンク と コピー の違いは、ファイルシステムにおけるファイルの参照やデータの扱い方にあります。

ハードリンクとは
	•	同じファイルデータ を指す 別名（参照）のようなものです。
	•	ハードリンクは 同じiノード（ファイルのメタデータとデータを含む）を共有します。
	•	実際のファイルデータは1つですが、複数のパスや名前から参照できます。

ハードリンクの特徴
	1.	データは共有される:
	•	元のファイルとハードリンクは 同じデータブロック を指します。
	2.	サイズを消費しない:
	•	新しいハードリンクを作成しても、データを複製しないため ディスク容量 は増えません。
	3.	削除してもデータは残る:
	•	元のファイルを削除しても、ハードリンクが残っていればデータは消えません。
	•	すべてのリンクが削除されたときに初めてデータが削除されます。
	4.	同じファイルシステム内でのみ利用可能:
	•	異なるファイルシステムや別のパーティションには作成できません。

ハードリンクの作成方法

ln existing_file hardlink_name

例:

ln file.txt hardlink.txt

	•	file.txt と hardlink.txt は同じデータを共有します。

コピーとは
	•	データの完全な複製 を新しいファイルとして作成します。
	•	コピー元とコピー先は 異なるiノード を持ち、それぞれ独立したファイルです。

コピーの特徴
	1.	データは複製される:
	•	コピー元とコピー先のデータは独立しています。
	2.	ディスク容量を消費する:
	•	コピーすると新しいデータブロックが作成されるため、ディスク容量 が増えます。
	3.	ファイルは独立している:
	•	片方を編集・削除しても、もう片方には影響しません。
	4.	異なるファイルシステム間でも利用可能:
	•	コピーは異なるディレクトリやパーティションにも自由に作成できます。

コピーの作成方法

cp existing_file copy_name

例:

cp file.txt copy.txt

	•	file.txt と copy.txt は独立したファイルになります。

ハードリンクとコピーの違いまとめ

項目	ハードリンク	コピー
データの共有	同じデータブロックを参照	完全に複製される
ディスク容量	増えない	増える
ファイルの独立性	独立していない（内容は共有）	独立している
削除の影響	すべてのリンクが削除されるまで残る	元のファイルが消えても影響なし
ファイルシステム	同一ファイルシステム内のみ	異なるファイルシステムも可

結論
	•	ハードリンク: データを共有し、ディスク容量を節約したい場合に使います。同じファイルの「別名」のようなものです。
	•	コピー: ファイルを独立させたい、または別の場所やファイルシステムに保存したい場合に使います。

用途に応じて使い分けると便利です！

## rpm の電子公開鍵ってなに

RPMの電子公開鍵は、RPMパッケージの信頼性と整合性を保証するために使用されるセキュリティ機能です。以下でその意味と役割を説明します。

1. 電子公開鍵とは
	•	電子公開鍵は、GPG（GNU Privacy Guard）鍵ペアの一部で、RPMパッケージの検証に使用されます。
	•	RPMパッケージの署名（rpm -K で確認可能）を検証し、そのパッケージが改ざんされていないことを確認するために利用します。

鍵ペアには次の2つがあります:
	1.	公開鍵（Public Key）: 誰でも利用可能で、署名の検証に使用。
	2.	秘密鍵（Private Key）: パッケージの署名を作成するために使用され、作成者が管理。

2. 電子公開鍵の役割

公開鍵は、次のような場面で重要な役割を果たします。
	1.	署名の検証:
	•	RPMパッケージはリポジトリや作成者によって**署名（デジタルシグネチャ）**されます。
	•	公開鍵を使って署名を検証することで、そのパッケージが改ざんされていないことを確認します。
	2.	信頼性の確認:
	•	公開鍵をインポートすると、そのリポジトリや提供元を信頼できることをシステムが認識します。
	•	不正なパッケージのインストールを防ぎます。

3. RPMの電子公開鍵の使用例

a. 公開鍵のインポート

RPMリポジトリを追加するとき、公開鍵をインポートする必要があります。通常は次のようなコマンドを実行します。

sudo rpm --import /path/to/public-key.gpg

例:
リポジトリから直接インポートする場合:

sudo rpm --import https://www.example.com/keys/RPM-GPG-KEY-example

b. RPMパッケージの署名を検証

インポートした公開鍵を使用して、RPMパッケージの署名を検証します。

署名の検証コマンド

rpm -K package.rpm

	•	出力例:
	•	gpg OK: 署名が正しく検証された。
	•	NOT OK: 署名が正しく検証されない（鍵が存在しない、またはパッケージが改ざんされている可能性）。

4. 公開鍵の確認

インポート済みの公開鍵を確認するには次のコマンドを使用します。

rpm -qa gpg-pubkey

公開鍵の詳細を確認するには:

rpm -qi gpg-pubkey-xxxxxxxx

	•	出力例:

Name        : gpg-pubkey
Version     : 6a2faea8
Release     : 5
Summary     : GPG key for Example Repo

5. 公開鍵がない場合のエラーと対応

RPMパッケージをインストールするとき、対応する公開鍵がインポートされていない場合、次のようなエラーが発生します。
	•	エラー例:

Public key for package.rpm is not installed


	•	解決方法:
	1.	パッケージ提供元が配布している公開鍵を取得。
	2.	次のコマンドで公開鍵をインポート:

sudo rpm --import /path/to/public-key.gpg

6. 公開鍵のセキュリティ上の注意
	•	公開鍵は信頼できるソース（公式ウェブサイトやリポジトリ）から取得してください。
	•	改ざんされた公開鍵を使用すると、不正なパッケージを信頼することになります。

まとめ
	•	RPMの電子公開鍵は、RPMパッケージの署名を検証し、そのパッケージが改ざんされていないことを保証するために使用されます。
	•	インポート: 公開鍵をインポートして信頼を確立。
	•	検証: 署名の整合性を確認して、安全なパッケージインストールを実現。

これにより、RPMパッケージのセキュリティを強化できます。 🚀

## rpm -qa gpg-pubkey　４つでてきたよ

rpm -qa gpg-pubkey コマンドで公開鍵が4つ出てきた場合、それはシステムに4つのGPG公開鍵がインポートされていることを意味します。これらはリポジトリやRPMパッケージの署名検証に使用されます。

公開鍵の確認手順
	1.	公開鍵のリストを確認
出力結果は次のような形式になります:

gpg-pubkey-xxxxxxxx-xxxxxxxx
gpg-pubkey-yyyyyyyy-yyyyyyyy
gpg-pubkey-zzzzzzzz-zzzzzzzz
gpg-pubkey-wwwwwwww-wwwwwwww

各公開鍵の形式:
	•	xxxxxxxx は公開鍵の識別子。
	•	yyyyyyyy は公開鍵がインポートされたタイムスタンプ。

	2.	公開鍵の詳細を表示
各公開鍵の詳細を確認するには次のコマンドを実行します:

rpm -qi gpg-pubkey-xxxxxxxx

例:

rpm -qi gpg-pubkey-6a2faea8

出力例:

Name        : gpg-pubkey
Version     : 6a2faea8
Release     : 5
Summary     : GPG key for Example Repo
Description :
Public key for verifying packages from Example Repository.
Packager    : Example Packager <packager@example.com>

	•	Summary: 鍵がどのリポジトリ用か説明されています。
	•	Packager: 公開鍵を作成したパッケージ提供者。

不要な鍵の削除

もし古い鍵や不要な鍵がインポートされている場合、削除することができます。
	1.	削除する鍵の識別子を確認
例: gpg-pubkey-6a2faea8
	2.	公開鍵を削除

sudo rpm -e gpg-pubkey-xxxxxxxx

例:

sudo rpm -e gpg-pubkey-6a2faea8

4つの鍵が存在する理由
	1.	複数のリポジトリが設定されている
	•	例えば、EPEL や CentOS Base、Remi などの異なるリポジトリが有効になっている場合、それぞれのリポジトリの公開鍵が必要です。
	2.	古い鍵が残っている
	•	以前使用されていたリポジトリや、アップデートで新しい鍵が提供された場合に古い鍵が残っていることがあります。

鍵が正しいか確認する必要性
	•	システムのセキュリティを確保するために、インポートされている公開鍵が信頼できるリポジトリやパッケージ提供者からのものであることを確認します。
	•	鍵の提供元が不明な場合、削除を検討してください。

まとめ
	1.	rpm -qa gpg-pubkey で公開鍵を確認。
	2.	rpm -qi gpg-pubkey-xxxxxxxx で詳細を確認。
	3.	必要に応じて sudo rpm -e gpg-pubkey-xxxxxxxx で不要な鍵を削除。

これでシステムにインポートされている公開鍵を管理し、安全性を確保できます！ 🚀

## centos でtar.gzの展開方法は

CentOSで.tar.gzファイルを展開するには、tarコマンドを使用します。以下に手順を示します。

手順

1. 基本的な展開コマンド

.tar.gzファイルを現在のディレクトリに展開するには、以下を実行します。

tar -xzvf filename.tar.gz

	•	オプションの意味:
	•	x: アーカイブの展開 (extract)
	•	z: gzip圧縮を解除 (gzip decompression)
	•	v: 展開時に詳細を表示 (verbose)
	•	f: ファイル名を指定 (file)

2. 展開先を指定

特定のディレクトリに展開したい場合は、-C オプションを使用します。

tar -xzvf filename.tar.gz -C /path/to/directory

	•	例: /opt/myfiles に展開する場合:

tar -xzvf filename.tar.gz -C /opt/myfiles

3. ファイル内容の確認

展開せずに .tar.gz ファイルの内容を確認したい場合は、-t オプションを使用します。

tar -tzvf filename.tar.gz

4. 圧縮されていない .tar ファイルの展開

もし .tar ファイルであれば、以下のコマンドで展開できます。

tar -xvf filename.tar

5. gzipのみを解凍

もしファイルが単なる .gz（アーカイブではないgzip圧縮ファイル）の場合、gunzip または tar を使用します。

gunzipを使用

gunzip filename.gz

tarを使用

tar -xzf filename.gz

6. インストールされていない場合

tar がインストールされていない場合は、以下のコマンドでインストールできます。

sudo yum install tar

使用例
	1.	展開

tar -xzvf example.tar.gz


	2.	内容確認

tar -tzvf example.tar.gz


	3.	特定のディレクトリに展開

tar -xzvf example.tar.gz -C /tmp

これで .tar.gz ファイルを簡単に展開できます！ 🚀

## PCI と、mother boardとは
## ssh した時の公開鍵、秘密鍵がどの様に使われてるか説明して
## known_hosts は存在したが、authorized_keysはない
## Xargs コマンドとは
## Xhost +するとどんなことが可能か
## VNC virtual network cloud とは
## grub とか　grub2って何？kernelとの違いは
## シェル変数と環境変数どういうこと
```
