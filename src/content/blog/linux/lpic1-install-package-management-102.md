---
author: Taro Gray
pubDatetime: 2025-02-09T08:00:00.000Z
title: Linuxのインストールとパッケージ管理(主題102)
postSlug: lpic1-install-package-management-102
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
description: lLinuxのインストールとパッケージ管理(主題102)
---

## Table of contents

---

author: Taro Gray
pubDatetime: 2025-01-31T08:00:00.000Z
title: RPM コマンドによるパッケージ管理
postSlug: linux-rpm-command
featured: true
tags:

- Linux
- RPM
  description: RPM コマンドを使用したパッケージのアップグレードとインストールの方法について解説

---

## RPM コマンドで「procmail」パッケージをアップグレードまたはインストールする方法

### **問題**

`rpm` コマンドを使用して、「procmail」パッケージを `procmail-3.22-9.i386.rpm` にアップグレードしたい。また、パッケージが存在しない場合はインストールしたい。適切なコマンドを選択せよ（複数選択可）。

### **選択肢**

- `rpm --upgrade procmail-3.22-9.i386.rpm`
- `rpm -F procmail-3.22-9.i386.rpm`
- `rpm -U procmail-3.22-9.i386.rpm`
- `rpm -e procmail`
- `rpm --freshen procmail-3.22-9.i386.rpm`

---

## **正解**

✅ `rpm -U procmail-3.22-9.i386.rpm`  
✅ `rpm --upgrade procmail-3.22-9.i386.rpm`

---

## **解説**

`rpm` コマンドは **RPM パッケージの管理**（インストール、アップグレード、アンインストールなど）を行うためのコマンドです。

### **RPM の主要なオプション**

| コマンド           | 説明                                                 |
| ------------------ | ---------------------------------------------------- |
| `-i` / `--install` | 新規インストール（すでにインストール済みならエラー） |
| `-U` / `--upgrade` | アップグレード（存在しない場合は新規インストール）   |
| `-F` / `--freshen` | アップグレードのみ（未インストールなら無視）         |
| `-e` / `--erase`   | 指定したパッケージを削除                             |
| `-q` / `--query`   | インストール済みパッケージの情報を取得               |

---

### **各選択肢の解説**

#### ✅ `rpm -U procmail-3.22-9.i386.rpm`

- **アップグレード** を実行し、パッケージが存在しない場合は **新規インストール** する。
- `-U` は `--upgrade` の省略形。

#### ✅ `rpm --upgrade procmail-3.22-9.i386.rpm`

- `-U` と同じ意味で、**アップグレードまたはインストール** を実行する。

#### ❌ `rpm -F procmail-3.22-9.i386.rpm`

- `-F` (`--freshen`) は、**すでにインストールされているパッケージのみアップグレード** する。
- **未インストールの場合は無視される** ため、今回の要件（存在しない場合はインストール）に適合しない。

#### ❌ `rpm -e procmail`

- `-e` (`--erase`) は、**パッケージを削除** するコマンド。
- **アップグレードやインストールとは無関係** のため不正解。

#### ❌ `rpm --freshen procmail-3.22-9.i386.rpm`

- `--freshen` は `-F` と同じく、**すでにインストール済みのパッケージのみアップグレード** する。
- **未インストールの場合は処理されない** ため不適切。

---

## **まとめ**

| コマンド                                 | 動作                                                       | 正誤 |
| ---------------------------------------- | ---------------------------------------------------------- | ---- |
| `rpm -U procmail-3.22-9.i386.rpm`        | アップグレード or 新規インストール                         | ✅   |
| `rpm --upgrade procmail-3.22-9.i386.rpm` | アップグレード or 新規インストール                         | ✅   |
| `rpm -F procmail-3.22-9.i386.rpm`        | インストール済みならアップグレード、未インストールなら無視 | ❌   |
| `rpm -e procmail`                        | パッケージの削除                                           | ❌   |
| `rpm --freshen procmail-3.22-9.i386.rpm` | インストール済みならアップグレード、未インストールなら無視 | ❌   |

### **💡 ポイント**

- `-U` または `--upgrade` は **アップグレード + インストール** の両方を実行可能。
- `-F` や `--freshen` は **未インストールの場合は無視** するため不適切。
- `-e` はアンインストールなので、今回の問題とは無関係。

✅ **RPM のアップグレード＆インストールには `rpm -U` または `rpm --upgrade` を使う！**

## RPM コマンドで「postfix」パッケージの検査を行う方法

### **問題**

`rpm` コマンドを使用して、「postfix」パッケージの検査を行いたい。ただし、MD5 によるファイルの改ざんの検査は行わないものとする。適切なコマンドを選択せよ（複数選択可）。

### **選択肢**

- `rpm -V --nomd5 postfix`
- `rpm -V postfix`
- `rpm -qc postfix`
- `rpm --verify --nomd5 postfix`
- `rpm --verify postfix`

---

## **正解**

✅ `rpm -V --nomd5 postfix`  
✅ `rpm --verify --nomd5 postfix`

---

## **解説**

`rpm` コマンドは **RPM パッケージの管理**（インストール、アンインストール、検査など）を行うためのコマンドです。

### **RPM の検査関連オプション**

| コマンド          | 説明                                               |
| ----------------- | -------------------------------------------------- |
| `-V` / `--verify` | インストール済みのパッケージを検査する             |
| `--nomd5`         | MD5 チェックサムによる検査を省略する               |
| `-q`              | インストール済みのパッケージ情報を取得             |
| `-qc`             | インストール済みパッケージの設定ファイル一覧を表示 |

---

### **各選択肢の解説**

#### ✅ `rpm -V --nomd5 postfix`

- `-V` (`--verify`) を使用して **postfix パッケージの整合性検査** を行う。
- `--nomd5` を指定することで **MD5 チェックサムによる改ざんチェックを省略** する。

#### ✅ `rpm --verify --nomd5 postfix`

- `-V` の代わりに `--verify` を使用して、**同じ動作** を行う。
- `--nomd5` により **MD5 チェックを行わずに検査** する。

#### ❌ `rpm -V postfix`

- `-V` (`--verify`) による検査は行うが、**MD5 チェックも実施する** ため問題の条件に合わない。

#### ❌ `rpm -qc postfix`

- `-q` (`--query`) オプションの `-c` は **設定ファイルの一覧を表示する** ためのものであり、検査ではない。

#### ❌ `rpm --verify postfix`

- `--verify` による検査は行うが、**MD5 チェックも実施する** ため問題の条件に合わない。

---

## **RPM の検査結果の見方**

`rpm -V postfix` または `rpm --verify postfix` を実行すると、変更されたファイルがある場合、以下のように表示される。

```sh
S.5....T.  c /etc/postfix/main.cf

文字	意味
S	ファイルサイズが変更されている
5	MD5 チェックサムが異なっている
T	修正時刻が異なっている
c	設定ファイルであることを示す

まとめ

コマンド	動作	正誤
rpm -V --nomd5 postfix	MD5 チェックなしでパッケージを検査	✅
rpm --verify --nomd5 postfix	MD5 チェックなしでパッケージを検査	✅
rpm -V postfix	MD5 チェックを含めてパッケージを検査	❌
rpm -qc postfix	設定ファイルの一覧を表示（検査ではない）	❌
rpm --verify postfix	MD5 チェックを含めてパッケージを検査	❌

💡 ポイント
	•	-V または --verify は インストール済みパッケージの検査 に使用する。
	•	--nomd5 を指定すると MD5 チェックなしで検査 を実行できる。
	•	設定ファイルの一覧を表示する rpm -qc は 検査ではない ので注意。

✅ RPM の検査には rpm -V --nomd5 または rpm --verify --nomd5 を使う！

RPM コマンドで「postfix」パッケージの変更履歴を調べる方法

問題

rpm コマンドを使用して、インストールされている「postfix」パッケージの変更履歴を調べたい。適切なコマンドを選択せよ（複数選択可）。

選択肢
	•	rpm --query --changelog postfix
	•	rpm -qi postfix
	•	rpm -q --log postfix
	•	rpm --query --log postfix
	•	rpm -q --changelog postfix

正解

✅ rpm -q --changelog postfix
✅ rpm --query --changelog postfix

解説

rpm コマンドは RPM パッケージの管理（インストール、アンインストール、情報表示など）を行うためのコマンドです。

RPM の情報取得関連オプション

コマンド	説明
-q / --query	インストール済みのパッケージ情報を取得
--changelog	変更履歴（Changelog）を表示
-qi	詳細なパッケージ情報を表示
--log	ログを表示（無効なオプション）

各選択肢の解説

✅ rpm -q --changelog postfix
	•	-q (--query) で postfix の情報を取得。
	•	--changelog で 変更履歴（Changelog）を表示 する。

✅ rpm --query --changelog postfix
	•	-q の代わりに --query を使用して、同じ動作 を行う。
	•	--changelog により 変更履歴を取得 できる。

❌ rpm -qi postfix
	•	-qi は パッケージの詳細情報 を表示するコマンドであり、変更履歴の確認には適さない。

❌ rpm -q --log postfix
	•	--log オプションは RPM には存在しない ためエラーになる。

❌ rpm --query --log postfix
	•	--log オプションは RPM には存在しない ためエラーになる。

RPM の Changelog の出力例

以下のコマンドを実行すると、パッケージの変更履歴を表示できる。

rpm -q --changelog postfix

出力例:

* Mon Feb 12 2024 John Doe <johndoe@example.com> - 3.6.1-2
- Bug fix: Fixed issue with TLS handshake

* Tue Jan 15 2023 Jane Smith <janesmith@example.com> - 3.6.0-1
- Updated to version 3.6.0
- Improved logging for SMTP connections

まとめ

コマンド	動作	正誤
rpm -q --changelog postfix	postfix の変更履歴を表示	✅
rpm --query --changelog postfix	postfix の変更履歴を表示	✅
rpm -qi postfix	パッケージの詳細情報を表示（Changelog は含まれない）	❌
rpm -q --log postfix	--log は無効なオプション	❌
rpm --query --log postfix	--log は無効なオプション	❌

💡 ポイント
	•	-q --changelog または --query --changelog で パッケージの変更履歴を表示 できる。
	•	-qi は詳細情報を表示するが、変更履歴は含まれない ため不適切。
	•	--log オプションは RPM には存在しない ため使用不可。

✅ RPM の変更履歴を確認するには rpm -q --changelog または rpm --query --changelog を使う！

```
