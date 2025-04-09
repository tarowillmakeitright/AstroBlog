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

### **正解**

✅ `rpm -U procmail-3.22-9.i386.rpm`  
✅ `rpm --upgrade procmail-3.22-9.i386.rpm`

---

### **解説**

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

### **まとめ**

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

## **RPM コマンドで「postfix-1.1.12-1.i386.rpm」の設定ファイルのみを表示する方法**

### **問題**

`rpm` コマンドを使用して、**「postfix-1.1.12-1.i386.rpm」ファイルからインストールされる設定ファイルのみ** を表示したい。  
適切なコマンドを選択せよ。

### **選択肢**

- `rpm -qcp postfix-1.1.12-1.i386.rpm`
- `rpm -qlp postfix-1.1.12-1.i386.rpm`
- `rpm --query --list --package postfix-1.1.12-1.i386.rpm`
- `rpm --query --list postfix`
- `rpm --query -cp postfix-1.1.12-1.i386.rpm`

---

### **正解**

✅ `rpm -qcp postfix-1.1.12-1.i386.rpm`  
✅ `rpm --query -cp postfix-1.1.12-1.i386.rpm`

---

### **解説**

`rpm` コマンドは、**RPM パッケージの情報を取得・管理** するために使用されます。

- `-q` (`--query`) → **パッケージ情報を取得**
- `-c` (`--configfiles`) → **設定ファイルのみを表示**
- `-p` (`--package`) → **インストール済みではなく、指定した RPM ファイルを対象にする**

### **設定ファイルのみを表示するには？**

| コマンド                          | 説明                                                                       |
| --------------------------------- | -------------------------------------------------------------------------- |
| `rpm -qc <パッケージ名>`          | **インストール済みのパッケージの設定ファイルを表示**                       |
| `rpm -qcp <RPMファイル名>`        | **指定した RPM ファイルの設定ファイルを表示**                              |
| `rpm --query -cp <RPMファイル名>` | **指定した RPM ファイルの設定ファイルを表示**（`-qcp` のロングオプション） |

---

### **各選択肢の解説**

#### ✅ `rpm -qcp postfix-1.1.12-1.i386.rpm`

- **指定した RPM ファイルに含まれる設定ファイルのみを表示** する。
- `-q` → **問い合わせ（query）**
- `-c` → **設定ファイルのみを表示**
- `-p` → **指定した RPM ファイルを対象**
- **正しいコマンド！**

実行例:

```sh
$ rpm -qcp postfix-1.1.12-1.i386.rpm
/etc/postfix/main.cf
/etc/postfix/master.cf
```

✅ rpm --query -cp postfix-1.1.12-1.i386.rpm

- rpm -qcp のロングオプション版（動作は同じ）
- 正しいコマンド！

❌ rpm -qlp postfix-1.1.12-1.i386.rpm

- 指定した RPM ファイルに含まれるすべてのファイルを一覧表示 する。
- 設定ファイルだけではなく、バイナリやドキュメントも含まれるため不適切。
- 不正解！

実行例:

```
$ rpm -qlp postfix-1.1.12-1.i386.rpm
/usr/sbin/postfix
/usr/libexec/postfix
/etc/postfix/main.cf
/etc/postfix/master.cf
/var/spool/postfix
```

...

（設定ファイル以外も含まれているため NG）

❌ rpm --query --list --package postfix-1.1.12-1.i386.rpm

- 指定した RPM ファイルのすべてのファイルを一覧表示する
- 設定ファイルのみを表示するわけではないため不適切
- 不正解！

実行例:

```
$ rpm --query --list --package postfix-1.1.12-1.i386.rpm
/usr/sbin/postfix
/usr/libexec/postfix
/etc/postfix/main.cf
/etc/postfix/master.cf
```

（設定ファイルだけでなく、すべてのファイルが表示されるため NG）

❌ rpm --query --list postfix

- インストール済みの postfix パッケージに含まれるすべてのファイルを一覧表示する
- 設定ファイルだけではなく、すべてのファイルが含まれるため不適切
- 不正解！

実行例:

```
$ rpm --query --list postfix
/usr/sbin/postfix
/usr/libexec/postfix
/etc/postfix/main.cf
/etc/postfix/master.cf
```

...

### まとめ

```
コマンド 説明 正誤
rpm -qcp postfix-1.1.12-1.i386.rpm 指定した RPM ファイルの設定ファイルのみを表示 ✅
rpm --query -cp postfix-1.1.12-1.i386.rpm 指定した RPM ファイルの設定ファイルのみを表示（ロングオプション） ✅
rpm -qlp postfix-1.1.12-1.i386.rpm 指定した RPM ファイルのすべてのファイルを一覧表示（設定ファイルのみではない） ❌
rpm --query --list --package postfix-1.1.12-1.i386.rpm 指定した RPM ファイルのすべてのファイルを一覧表示 ❌
rpm --query --list postfix インストール済みの postfix に含まれるすべてのファイルを表示 ❌
```

💡 ポイント

- 設定ファイルのみを表示するには -qcp または --query -cp を使う！ ✅
- すべてのファイルを表示する -qlp, --query --list は不適切！ ❌

✅ RPM ファイル内の設定ファイルを確認するなら rpm -qcp <RPMファイル名>！

##RPM コマンドで「postfix」パッケージの変更履歴を調べる方法

### 問題

rpm コマンドを使用して、インストールされている「postfix」パッケージの変更履歴を調べたい。適切なコマンドを選択せよ（複数選択可）。

選択肢

- rpm --query --changelog postfix
- rpm -qi postfix
- rpm -q --log postfix
- rpm --query --log postfix
- rpm -q --changelog postfix

### 正解

✅ rpm -q --changelog postfix
✅ rpm --query --changelog postfix

### 解説

rpm コマンドは RPM パッケージの管理（インストール、アンインストール、情報表示など）を行うためのコマンドです。

RPM の情報取得関連オプション

コマンド 説明
-q / --query インストール済みのパッケージ情報を取得
--changelog 変更履歴（Changelog）を表示
-qi 詳細なパッケージ情報を表示
--log ログを表示（無効なオプション）

各選択肢の解説

✅ rpm -q --changelog postfix

- -q (--query) で postfix の情報を取得。
- --changelog で 変更履歴（Changelog）を表示 する。

✅ rpm --query --changelog postfix

- -q の代わりに --query を使用して、同じ動作 を行う。
- --changelog により 変更履歴を取得 できる。

❌ rpm -qi postfix

- -qi は パッケージの詳細情報 を表示するコマンドであり、変更履歴の確認には適さない。

❌ rpm -q --log postfix

- --log オプションは RPM には存在しない ためエラーになる。

❌ rpm --query --log postfix

- --log オプションは RPM には存在しない ためエラーになる。

RPM の Changelog の出力例

以下のコマンドを実行すると、パッケージの変更履歴を表示できる。

rpm -q --changelog postfix

出力例:

- Mon Feb 12 2024 John Doe <johndoe@example.com> - 3.6.1-2

* Bug fix: Fixed issue with TLS handshake

- Tue Jan 15 2023 Jane Smith <janesmith@example.com> - 3.6.0-1

* Updated to version 3.6.0
* Improved logging for SMTP connections

### まとめ

```
コマンド 動作 正誤
rpm -q --changelog postfix postfix の変更履歴を表示 ✅
rpm --query --changelog postfix postfix の変更履歴を表示 ✅
rpm -qi postfix パッケージの詳細情報を表示（Changelog は含まれない） ❌
rpm -q --log postfix --log は無効なオプション ❌
rpm --query --log postfix --log は無効なオプション ❌
```

...

💡 ポイント

- -q --changelog または --query --changelog で パッケージの変更履歴を表示 できる。
- -qi は詳細情報を表示するが、変更履歴は含まれない ため不適切。
- --log オプションは RPM には存在しない ため使用不可。

✅ RPM の変更履歴を確認するには rpm -q --changelog または rpm --query --changelog を使う！

YUM コマンドで「yum」を含むパッケージを検索する方法

### 問題

yum コマンドを使用して、キーワード「yum」を含むパッケージを表示させたい。適切なコマンドを選択せよ。

選択肢

- yum show yum
- yum search yum
- yum -s yum
- yum list yum
- yum info yum

### 正解

✅ yum search yum

### 解説

yum コマンドは RPM パッケージ管理ツール であり、パッケージのインストールや検索、更新、削除などを行うために使用されます。

YUM の主なパッケージ検索関連オプション

コマンド 説明
yum search <キーワード> 指定したキーワードを含むパッケージを検索
yum list <パッケージ名> 指定したパッケージのインストール状況を確認
yum info <パッケージ名> 指定したパッケージの詳細情報を表示

各選択肢の解説

✅ yum search yum

- yum search <キーワード> は 指定したキーワードを含むパッケージを検索 するためのコマンド。
- yum search yum を実行すると、「yum」が名前や説明に含まれるすべてのパッケージを一覧表示する。

実行例

yum search yum

出力例

=========================== Name & Summary Matched: yum ===========================
yum.noarch : RPM package manager
yum-utils.noarch : Utilities based around the yum package manager

❌ yum show yum

- show オプションは yum には存在しないため、エラー になる。

❌ yum -s yum

- -s というオプションは yum には存在しないため、エラー になる。

❌ yum list yum

- yum list <パッケージ名> は 指定したパッケージのリストを表示 するが、部分一致の検索には対応していない。
- そのため、「yum」という文字列を含むすべてのパッケージは表示されない。

❌ yum info yum

- yum info <パッケージ名> は 指定したパッケージの詳細情報を表示 するためのコマンド。
- yum という特定のパッケージの情報は得られるが、「yum」を含むすべてのパッケージを検索するわけではない。

### まとめ

```
コマンド 動作 正誤
yum search yum 「yum」を含むパッケージを検索 ✅
yum show yum show は無効なオプション（エラー） ❌
yum -s yum -s は無効なオプション（エラー） ❌
yum list yum yum というパッケージのリストを表示（部分一致の検索は不可） ❌
yum info yum yum というパッケージの詳細情報を表示 ❌
```

💡 ポイント

- yum search <キーワード> → キーワードを含むすべてのパッケージを検索する（今回の正解）。
- yum list <パッケージ名> → 指定したパッケージのインストール状況を確認する。
- yum info <パッケージ名> → 指定したパッケージの詳細情報を確認する。

✅ 「yum」を含むパッケージを検索するには yum search yum を使う！

## RPM コマンドで「procmail-3.22-9.i386.rpm」パッケージをインストールする方法

### **問題**

`rpm` コマンドを使用して、「procmail-3.22-9.i386.rpm」パッケージをインストールしたい。  
ただし、元々「procmail」がインストールされていない場合、実行可能なコマンドを選択せよ（複数選択可）。

### **選択肢**

- `rpm -F procmail-3.22-9.i386.rpm`
- `rpm -i procmail`
- `rpm -U procmail`
- `rpm -U procmail-3.22-9.i386.rpm`
- `rpm -i procmail-3.22-9.i386.rpm`

---

### **正解**

✅ `rpm -U procmail-3.22-9.i386.rpm`  
✅ `rpm -i procmail-3.22-9.i386.rpm`

---

### **解説**

`rpm` コマンドは、**RPM パッケージの管理**（インストール、アップグレード、削除、検査など）を行うためのツールです。

### **RPM のインストール関連オプション**

| コマンド           | 説明                                                       |
| ------------------ | ---------------------------------------------------------- |
| `-i` (`--install`) | **新規インストール**（既存のバージョンがある場合はエラー） |
| `-U` (`--upgrade`) | **アップグレード（未インストール時は新規インストール）**   |
| `-F` (`--freshen`) | **アップグレードのみ（未インストール時は何もしない）**     |

---

### **各選択肢の解説**

#### ✅ `rpm -U procmail-3.22-9.i386.rpm`

- `-U`（`--upgrade`）は、パッケージがインストール済みなら **アップグレード** し、未インストールなら **新規インストール** する。
- **今回の条件（未インストール）ではインストールが可能なので正解！**

#### ✅ `rpm -i procmail-3.22-9.i386.rpm`

- `-i`（`--install`）は、新規インストール専用のオプション。
- パッケージが未インストールなら **そのままインストール可能**。
- **今回の条件（未インストール）では問題なくインストールできるので正解！**

#### ❌ `rpm -F procmail-3.22-9.i386.rpm`

- `-F`（`--freshen`）は、**パッケージが既にインストールされている場合のみ** アップグレードするオプション。
- **未インストールの状態では何もしないため、今回の条件では不適切！**

#### ❌ `rpm -i procmail`

- `-i` は **パッケージファイル（.rpm）を指定する必要がある**。
- ここでは `procmail` のみを指定しているため、**適切なパッケージを探せずエラーになる！**

#### ❌ `rpm -U procmail`

- `-U` も `-i` と同様に **パッケージファイル（.rpm）を指定する必要がある**。
- ここでは `procmail` のみを指定しているため、**適切なパッケージを探せずエラーになる！**

---

### **まとめ**

| コマンド                          | 動作                                                           | 正誤 |
| --------------------------------- | -------------------------------------------------------------- | ---- |
| `rpm -U procmail-3.22-9.i386.rpm` | 未インストールなら新規インストール、既にあるならアップグレード | ✅   |
| `rpm -i procmail-3.22-9.i386.rpm` | 新規インストール専用（今回の条件では問題なし）                 | ✅   |
| `rpm -F procmail-3.22-9.i386.rpm` | 既にインストールされていないと動作しない                       | ❌   |
| `rpm -i procmail`                 | `.rpm` ファイルを指定していないためエラー                      | ❌   |
| `rpm -U procmail`                 | `.rpm` ファイルを指定していないためエラー                      | ❌   |

---

### **💡 ポイント**

- `-i`（`--install`）は新規インストール専用。
- `-U`（`--upgrade`）は **未インストール時もインストールされる** ため `-i` の上位互換的な存在。
- `-F`（`--freshen`）は **すでにインストール済みのパッケージがないと実行されない**。

✅ **RPM パッケージをインストールするには `rpm -i` または `rpm -U` を使う！**

## RPM コマンドで「procmail-3.22-25.1.el6.i686.rpm」パッケージを新規インストールする際に進行状況を表示させる方法

### **問題**

`rpm` コマンドを使用して、「procmail-3.22-25.1.el6.i686.rpm」パッケージを新規インストールする際、**進行状況を表示** させたい。  
適切なコマンドを選択せよ（複数選択可）。

### **選択肢**

- `rpm -iv procmail-3.22-25.1.el6.i686.rpm`
- `rpm -i --hash procmail-3.22-25.1.el6.i686.rpm`
- `rpm -i --test procmail-3.22-25.1.el6.i686.rpm`
- `rpm -ih procmail-3.22-25.1.el6.i686.rpm`
- `rpm --install -v procmail-3.22-25.1.el6.i686.rpm`

---

### **正解**

✅ `rpm -iv procmail-3.22-25.1.el6.i686.rpm`  
✅ `rpm -ih procmail-3.22-25.1.el6.i686.rpm`  
✅ `rpm --install -v procmail-3.22-25.1.el6.i686.rpm`

---

### **解説**

`rpm` コマンドは、**RPM パッケージの管理**（インストール、アップグレード、削除、検査など）を行うためのツールです。

### **RPM の主なオプション**

| オプション         | 説明                                                       |
| ------------------ | ---------------------------------------------------------- |
| `-i` (`--install`) | **新規インストール**（既存のバージョンがある場合はエラー） |
| `-v` (`--verbose`) | **詳細情報を表示**                                         |
| `-h` (`--hash`)    | **進行状況をハッシュ（`#`）で表示**                        |
| `--test`           | **インストールのテストのみ（実際にはインストールしない）** |

---

### **各選択肢の解説**

#### ✅ `rpm -iv procmail-3.22-25.1.el6.i686.rpm`

- `-i`（`--install`）：新規インストール
- `-v`（`--verbose`）：インストール時の詳細情報を表示
- **進行状況（処理中のファイル情報など）が表示されるため正解！**

#### ✅ `rpm -ih procmail-3.22-25.1.el6.i686.rpm`

- `-i`（`--install`）：新規インストール
- `-h`（`--hash`）：進行状況を `#####` のようなハッシュで表示
- **ハッシュ記号による進行状況の可視化が可能なため正解！**

#### ✅ `rpm --install -v procmail-3.22-25.1.el6.i686.rpm`

- `--install`：新規インストール（`-i` と同じ）
- `-v`（`--verbose`）：詳細な進行状況を表示
- **進行状況を表示するため正解！**

#### ❌ `rpm -i --hash procmail-3.22-25.1.el6.i686.rpm`

- `--hash` は **存在しないオプション** なのでエラーになる。
- 正しいオプションは `-h` または `--hash` ではなく **`-ih`**。

#### ❌ `rpm -i --test procmail-3.22-25.1.el6.i686.rpm`

- `--test` は **インストールをシミュレーションする** オプションであり、実際にはインストールされない。
- **進行状況を表示するものではないため不適切！**

---

### **まとめ**

| コマンド                                           | 動作                      | 進行状況表示 | 正誤 |
| -------------------------------------------------- | ------------------------- | ------------ | ---- |
| `rpm -iv procmail-3.22-25.1.el6.i686.rpm`          | 詳細情報付きインストール  | ✅           | ✅   |
| `rpm -ih procmail-3.22-25.1.el6.i686.rpm`          | 進行状況をハッシュ表示    | ✅           | ✅   |
| `rpm --install -v procmail-3.22-25.1.el6.i686.rpm` | 詳細情報付きインストール  | ✅           | ✅   |
| `rpm -i --hash procmail-3.22-25.1.el6.i686.rpm`    | `--hash` オプションは無効 | ❌           | ❌   |
| `rpm -i --test procmail-3.22-25.1.el6.i686.rpm`    | インストールのテストのみ  | ❌           | ❌   |

---

### **💡 ポイント**

- `-i`（`--install`）は新規インストール専用。
- `-v`（`--verbose`）は **詳細な進行状況を表示**。
- `-h`（`--hash`）は **インストールの進行状況をハッシュで表示**。
- `--test` は **インストールのテストのみ** であり、実際のインストールはされない。

✅ **進行状況を表示するには `-v`（詳細情報）や `-h`（ハッシュ表示）を組み合わせる！**

## **Zypper コマンドでリポジトリを更新する方法**

### **問題**

`zypper` コマンドを使用して、**リポジトリを更新** したい。  
適切なコマンドを選択せよ。

### **選択肢**

- `zypper updaterep`
- `zypper list-updates`
- `zypper update`
- `zypper refresh`
- `zypper repos`

---

### **正解**

✅ `zypper refresh`

---

### **解説**

`zypper` は、openSUSE や SUSE Linux Enterprise (SLE) で使用されるパッケージ管理ツールです。  
リポジトリの更新（メタデータのリフレッシュ）には `refresh` オプションを使用します。

### **Zypper の主なリポジトリ関連コマンド**

| コマンド              | 説明                                                     |
| --------------------- | -------------------------------------------------------- |
| `zypper refresh`      | **リポジトリのメタデータを更新**                         |
| `zypper repos`        | **登録されているリポジトリの一覧を表示**                 |
| `zypper list-updates` | **利用可能なパッケージのアップデートを表示**             |
| `zypper update`       | **パッケージの更新を実行（リポジトリの更新とは異なる）** |

---

### **各選択肢の解説**

#### ✅ `zypper refresh`

- **リポジトリのメタデータを更新（キャッシュをリフレッシュ）** するコマンド。
- **パッケージリストの最新情報を取得** するため、リポジトリの更新にはこのコマンドが正しい。

#### ❌ `zypper updaterep`

- **このコマンドは存在しない** ためエラーになる。

#### ❌ `zypper list-updates`

- **リポジトリの更新ではなく、利用可能なアップデート一覧を表示** するコマンド。
- 例: `zypper list-updates` を実行すると、アップグレード可能なパッケージが一覧表示される。
- **リポジトリの更新とは無関係なので不適切！**

#### ❌ `zypper update`

- **パッケージのアップデートを行うコマンド**。
- 例えば、`zypper update` を実行すると、システム内の全パッケージが最新バージョンに更新される。
- **リポジトリのメタデータを更新するわけではないため不適切！**

#### ❌ `zypper repos`

- **登録されているリポジトリの一覧を表示するコマンド**。
- 例: `zypper repos` を実行すると、現在のリポジトリの一覧が表示される。
- **リポジトリのメタデータを更新するわけではないので不適切！**

---

### **まとめ**

| コマンド              | 動作                                   | 正誤 |
| --------------------- | -------------------------------------- | ---- |
| `zypper refresh`      | **リポジトリのメタデータを更新**       | ✅   |
| `zypper updaterep`    | **無効なコマンド（存在しない）**       | ❌   |
| `zypper list-updates` | **利用可能なアップデートを表示**       | ❌   |
| `zypper update`       | **パッケージの更新を実行**             | ❌   |
| `zypper repos`        | **登録されているリポジトリを一覧表示** | ❌   |

---

### **💡 ポイント**

- **リポジトリの更新 → `zypper refresh`** ✅
- **パッケージの一覧表示 → `zypper list-updates`** ❌
- **パッケージの更新 → `zypper update`** ❌
- **リポジトリの一覧表示 → `zypper repos`** ❌

✅ **リポジトリを更新するには `zypper refresh` を使う！**

## **Zypper コマンドで全てのパッケージをアップデートする方法**

### **問題**

`zypper` コマンドを使用して、**アップデート可能な全てのパッケージをアップデート** したい。  
適切なコマンドを 2 つ選択せよ。

### **選択肢**

- `zypper update`
- `zypper list-updates`
- `zypper up`
- `zypper --update`
- `zypper refresh`

---

### **正解**

✅ `zypper update`  
✅ `zypper up`

---

### **解説**

`zypper` は openSUSE や SUSE Linux Enterprise (SLE) で使用されるパッケージ管理ツールです。  
**システム内の全てのパッケージを最新のバージョンにアップデートするには `update` または `up` を使用** します。

### **Zypper の主なアップデート関連コマンド**

| コマンド              | 説明                                                         |
| --------------------- | ------------------------------------------------------------ |
| `zypper update`       | **全てのパッケージをアップデート**                           |
| `zypper up`           | **`zypper update` の短縮形（同じ動作）**                     |
| `zypper list-updates` | **アップデート可能なパッケージの一覧を表示（更新はしない）** |
| `zypper refresh`      | **リポジトリのメタデータを更新（パッケージの更新はしない）** |

---

### **各選択肢の解説**

#### ✅ `zypper update`

- **システム内のすべてのパッケージを最新バージョンにアップデートするコマンド。**
- `zypper update` は **インストール済みのパッケージを最新バージョンに更新** するため、今回の問題に適切。

#### ✅ `zypper up`

- **`zypper update` の短縮形** であり、**同じ動作をする**。
- `zypper update` を打つのが面倒な場合は `zypper up` でも同じ処理ができるため正解！

#### ❌ `zypper list-updates`

- **アップデート可能なパッケージの一覧を表示するコマンド**。
- 例: `zypper list-updates` を実行すると、更新可能なパッケージのリストが表示されるが **実際にアップデートはしない**。
- **アップデートを実行するわけではないため不適切！**

#### ❌ `zypper --update`

- **このコマンドは存在しない** ためエラーになる。

#### ❌ `zypper refresh`

- **リポジトリのメタデータを更新するコマンド** であり、パッケージの更新はしない。
- **アップデートの準備としては重要** だが、パッケージのアップデート自体は行わないため不適切！

---

### **まとめ**

| コマンド              | 動作                                                         | 正誤 |
| --------------------- | ------------------------------------------------------------ | ---- |
| `zypper update`       | **全パッケージをアップデート**                               | ✅   |
| `zypper up`           | **`zypper update` の短縮形（全パッケージ更新）**             | ✅   |
| `zypper list-updates` | **アップデート可能なパッケージ一覧を表示**                   | ❌   |
| `zypper --update`     | **無効なコマンド（存在しない）**                             | ❌   |
| `zypper refresh`      | **リポジトリのメタデータを更新（パッケージの更新はしない）** | ❌   |

---

### **💡 ポイント**

- **全パッケージをアップデート → `zypper update` または `zypper up`** ✅
- **更新可能なパッケージを確認 → `zypper list-updates`** ❌
- **リポジトリの更新 → `zypper refresh`** ❌

✅ **パッケージを最新にするには `zypper update` または `zypper up` を使う！**

## **Yum コマンドでパッケージグループを一覧表示する方法**

### **問題**

`yum` コマンドを使用して、**パッケージグループを一覧表示** させたい。  
適切なコマンドを選択せよ。

### **選択肢**

- `yum packagegroup`
- `yum group-list`
- `yum group`
- `yum package-group`
- `yum grouplist`

---

### **正解**

✅ `yum grouplist`

---

### **解説**

`yum` コマンドは、RPM パッケージを管理するツールです。  
パッケージグループの一覧を表示するには `grouplist` を使用します。

### **パッケージグループとは？**

- **関連するパッケージをまとめたグループ**。
- 例: `"Development Tools"` をインストールすると、`gcc`, `make`, `automake` などの開発関連ツールが一括インストールされる。

### **パッケージグループ関連コマンド**

| コマンド                          | 説明                                                  |
| --------------------------------- | ----------------------------------------------------- |
| `yum grouplist`                   | **パッケージグループの一覧を表示（最新のYumで使用）** |
| `yum groupinfo "<グループ名>"`    | **指定したパッケージグループの詳細を表示**            |
| `yum groupinstall "<グループ名>"` | **指定したパッケージグループをインストール**          |
| `yum groupremove "<グループ名>"`  | **指定したパッケージグループを削除**                  |

---

### **各選択肢の解説**

#### ✅ `yum grouplist`

- **最新の Yum でパッケージグループの一覧を表示するコマンド**。
- `yum grouplist` を実行すると、**利用可能なパッケージグループが一覧表示される**。

#### ❌ `yum packagegroup`

- **このコマンドは存在しない** ためエラーになる。

#### ❌ `yum group-list`

- **このコマンドは無効**。  
  一部の古いドキュメントには記載されているが、**現在の Yum では使われていない**。

#### ❌ `yum group`

- **このコマンドは無効** であり、エラーになる。

#### ❌ `yum package-group`

- **このコマンドも存在しないためエラーになる**。

---

### **まとめ**

| コマンド            | 動作                                                 | 正誤 |
| ------------------- | ---------------------------------------------------- | ---- |
| `yum grouplist`     | **パッケージグループの一覧を表示（最新バージョン）** | ✅   |
| `yum packagegroup`  | **無効なコマンド（存在しない）**                     | ❌   |
| `yum group-list`    | **無効なコマンド（現在のYumでは使われない）**        | ❌   |
| `yum group`         | **無効なコマンド（存在しない）**                     | ❌   |
| `yum package-group` | **無効なコマンド（存在しない）**                     | ❌   |

---

### **💡 ポイント**

- **パッケージグループの一覧 → `yum grouplist` を使う！** ✅
- **`yum packagegroup`, `yum group-list`, `yum group`, `yum package-group` は無効！** ❌

✅ **パッケージグループを一覧表示するには `yum grouplist` を使おう！**

## **RPM コマンドで「postfix」パッケージのインストール状況を確認する方法**

### **問題**

`rpm` コマンドを使用して、**「postfix」パッケージがインストールされているかどうか** 確認したい。  
また、**余計な情報を出力しない** 適切なコマンドを選択せよ。

### **選択肢**

- `rpm -ql postfix`
- `rpm -q postfix`
- `rpm --query -a`
- `rpm -qa`
- `rpm --query postfix`

---

### **正解**

✅ `rpm -q postfix`  
✅ `rpm --query postfix`

---

### **解説**

`rpm` コマンドは、**RPM パッケージのインストール状況を確認** するために使用されます。

- **インストール済みかどうかを確認するには `rpm -q <パッケージ名>` を使用**
- **`-q` は `--query` の省略形**

### **各コマンドの動作**

| コマンド              | 説明                                                                        | 正誤 |
| --------------------- | --------------------------------------------------------------------------- | ---- |
| `rpm -q postfix`      | **postfix がインストールされているか確認**（余計な情報なし）                | ✅   |
| `rpm --query postfix` | **postfix がインストールされているか確認**（`-q` のロングオプション）       | ✅   |
| `rpm -ql postfix`     | **インストールされている postfix のファイル一覧を表示**（余計な情報が出る） | ❌   |
| `rpm --query -a`      | **すべてのインストール済みパッケージを一覧表示**（余計な情報が出る）        | ❌   |
| `rpm -qa`             | **すべてのインストール済みパッケージを一覧表示**（余計な情報が出る）        | ❌   |

---

### **詳細な解説**

#### ✅ `rpm -q postfix`

- `-q` は `--query` の短縮形で、**指定したパッケージがインストールされているかを確認** する。
- **余計な情報を表示せず、パッケージ名だけを出力**。

実行例（postfix がインストールされている場合）:

```sh
$ rpm -q postfix
postfix-3.5.8-1.el8.x86_64
```

（インストールされている場合はバージョン情報が表示される）

✅ rpm --query postfix

- -q のロングオプション版。
- 動作は rpm -q postfix とまったく同じ。

❌ rpm -ql postfix

- -ql は --query --list の短縮形で、パッケージがインストールしているファイルの一覧を表示 する。
- 単にインストールの有無を確認するには余計な情報が多い ため不適切。

実行例:

```
$ rpm -ql postfix
/etc/postfix
/etc/postfix/main.cf
/usr/libexec/postfix
```

...

❌ rpm --query -a

- -a は --all の略で、すべてのインストール済みパッケージを一覧表示 する。
- postfix だけを確認するには不適切（不要な情報が多すぎる）。

実行例:

```
$ rpm --query -a
bash-5.0.17-1.el8.x86_64
coreutils-8.30-6.el8.x86_64
postfix-3.5.8-1.el8.x86_64
```

...

❌ rpm -qa

- -qa は --query --all の略で、すべてのインストール済みパッケージを一覧表示 する。
- 特定のパッケージ（postfix）だけを知りたい場合には不適切。

### まとめ

```
コマンド 説明 正誤
rpm -q postfix postfix がインストールされているか確認（余計な情報なし） ✅
rpm --query postfix postfix がインストールされているか確認（-q のロングオプション） ✅
rpm -ql postfix postfix のインストール済みファイル一覧を表示（情報が多すぎる） ❌
rpm --query -a すべてのインストール済みパッケージを一覧表示（情報が多すぎる） ❌
rpm -qa すべてのインストール済みパッケージを一覧表示（情報が多すぎる） ❌
```

💡 ポイント

- postfix がインストールされているか確認するには rpm -q postfix または rpm --query postfix ✅
- すべてのパッケージを確認する場合は rpm -qa や rpm --query -a（今回は不適切） ❌
- インストール済みのファイルを確認する場合は rpm -ql postfix（今回は不適切） ❌

✅ RPM パッケージがインストールされているかを確認するなら rpm -q postfix！

## **RPM コマンドで「postfix-1.1.12-1.i386.rpm」の設定ファイルのみを表示する方法**

### **問題**

`rpm` コマンドを使用して、**「postfix-1.1.12-1.i386.rpm」ファイルからインストールされる設定ファイルのみ** を表示したい。
適切なコマンドを選択せよ。

### **選択肢**

- `rpm -qcp postfix-1.1.12-1.i386.rpm`
- `rpm -qlp postfix-1.1.12-1.i386.rpm`
- `rpm --query --list --package postfix-1.1.12-1.i386.rpm`
- `rpm --query --list postfix`
- `rpm --query -cp postfix-1.1.12-1.i386.rpm`

---

### **正解**

✅ `rpm -qcp postfix-1.1.12-1.i386.rpm`
✅ `rpm --query -cp postfix-1.1.12-1.i386.rpm`

---

### **解説**

`rpm` コマンドは、**RPM パッケージの情報を取得・管理** するために使用されます。

- `-q` (`--query`) → **パッケージ情報を取得**
- `-c` (`--configfiles`) → **設定ファイルのみを表示**
- `-p` (`--package`) → **インストール済みではなく、指定した RPM ファイルを対象にする**

### **設定ファイルのみを表示するには？**

| コマンド                          | 説明                                                                       |
| --------------------------------- | -------------------------------------------------------------------------- |
| `rpm -qc <パッケージ名>`          | **インストール済みのパッケージの設定ファイルを表示**                       |
| `rpm -qcp <RPMファイル名>`        | **指定した RPM ファイルの設定ファイルを表示**                              |
| `rpm --query -cp <RPMファイル名>` | **指定した RPM ファイルの設定ファイルを表示**（`-qcp` のロングオプション） |

---

### **各選択肢の解説**

#### ✅ `rpm -qcp postfix-1.1.12-1.i386.rpm`

- **指定した RPM ファイルに含まれる設定ファイルのみを表示** する。
- `-q` → **問い合わせ（query）**
- `-c` → **設定ファイルのみを表示**
- `-p` → **指定した RPM ファイルを対象**
- **正しいコマンド！**

実行例:

```
$ rpm -qcp postfix-1.1.12-1.i386.rpm
/etc/postfix/main.cf
/etc/postfix/master.cf
```

...
✅ rpm --query -cp postfix-1.1.12-1.i386.rpm

- rpm -qcp のロングオプション版（動作は同じ）
- 正しいコマンド！

❌ rpm -qlp postfix-1.1.12-1.i386.rpm

- 指定した RPM ファイルに含まれるすべてのファイルを一覧表示 する。
- 設定ファイルだけではなく、バイナリやドキュメントも含まれるため不適切。
- 不正解！

実行例:

```
$ rpm -qlp postfix-1.1.12-1.i386.rpm
/usr/sbin/postfix
/usr/libexec/postfix
/etc/postfix/main.cf
/etc/postfix/master.cf
/var/spool/postfix
```

...

（設定ファイル以外も含まれているため NG）

❌ rpm --query --list --package postfix-1.1.12-1.i386.rpm

- 指定した RPM ファイルのすべてのファイルを一覧表示する
- 設定ファイルのみを表示するわけではないため不適切
- 不正解！

実行例:

```
$ rpm --query --list --package postfix-1.1.12-1.i386.rpm
/usr/sbin/postfix
/usr/libexec/postfix
/etc/postfix/main.cf
/etc/postfix/master.cf
```

...

（設定ファイルだけでなく、すべてのファイルが表示されるため NG）

❌ rpm --query --list postfix

- インストール済みの postfix パッケージに含まれるすべてのファイルを一覧表示する
- 設定ファイルだけではなく、すべてのファイルが含まれるため不適切
- 不正解！

実行例:

```
$ rpm --query --list postfix
/usr/sbin/postfix
/usr/libexec/postfix
/etc/postfix/main.cf
/etc/postfix/master.cf
```

...

### まとめ

```
コマンド 説明 正誤
rpm -qcp postfix-1.1.12-1.i386.rpm 指定した RPM ファイルの設定ファイルのみを表示 ✅
rpm --query -cp postfix-1.1.12-1.i386.rpm 指定した RPM ファイルの設定ファイルのみを表示（ロングオプション） ✅
rpm -qlp postfix-1.1.12-1.i386.rpm 指定した RPM ファイルのすべてのファイルを一覧表示（設定ファイルのみではない） ❌
rpm --query --list --package postfix-1.1.12-1.i386.rpm 指定した RPM ファイルのすべてのファイルを一覧表示 ❌
rpm --query --list postfix インストール済みの postfix に含まれるすべてのファイルを表示 ❌
```

💡 ポイント

- 設定ファイルのみを表示するには -qcp または --query -cp を使う！ ✅
- すべてのファイルを表示する -qlp, --query --list は不適切！ ❌

✅ RPM ファイル内の設定ファイルを確認するなら rpm -qcp <RPMファイル名>！

## **find コマンドの出力とエラーをファイルに保存する方法**

### **問題**

`find` コマンドの実行結果とエラー出力を、**どちらも `find.log` ファイルに保存** したい。  
適切なコマンドを選択せよ。

### **選択肢**

1. `find / -name core > find.log`
2. `find / -name core 2 >> find.log`
3. `find / -name core 2 >& 1 | find.log`
4. `find / -name core > find.log 2>&1`
5. `find / -name core 2>&1 find.log`

---

### **正解**

✅ **`find / -name core > find.log 2>&1`**（D）

---

### **解説**

`find` コマンドは、指定したディレクトリ内でファイルを検索するためのコマンドです。  
検索時に発生する **エラー出力（標準エラー `stderr`）** もあるため、標準出力 `stdout` だけでなく **`stderr` もファイルにリダイレクトする** 必要があります。

### **リダイレクトの基本**

| 記号   | 説明                                         |
| ------ | -------------------------------------------- |
| `>`    | 標準出力（stdout）をファイルにリダイレクト   |
| `>>`   | 標準出力をファイルに追記                     |
| `2>`   | 標準エラー（stderr）をファイルにリダイレクト |
| `2>>`  | 標準エラーをファイルに追記                   |
| `2>&1` | 標準エラー（2）を標準出力（1）にマージ       |

---

### **各選択肢の解説**

### ❌ A. `find / -name core > find.log`

- `>` は **標準出力（stdout）** のみを `find.log` にリダイレクトする。
- **標準エラー（stderr）は出力されないため不適切**。

---

### ❌ B. `find / -name core 2 >> find.log`

- `2 >> find.log` は **標準エラー（stderr）を `find.log` に追記する** という意味。
- **標準出力（stdout）はリダイレクトされていないため、不適切**。

---

### ❌ C. `find / -name core 2 >& 1 | find.log`

- `2 >& 1` は **標準エラー（stderr）を標準出力（stdout）にマージ** する。
- しかし、`| find.log` の部分が無効な構文であり、正しく動作しない。

---

### ✅ D. `find / -name core > find.log 2>&1`

- `> find.log` → **標準出力（stdout）を `find.log` に保存**
- `2>&1` → **標準エラー（stderr）を標準出力（stdout）にマージ**
- これにより、**stdout と stderr の両方が `find.log` に記録される**。
- **✅ 正しいコマンド！**

実行例:

```sh
find / -name core > find.log 2>&1
```

結果:

- find.log に find コマンドの 検索結果（stdout） と エラーメッセージ（stderr） の両方が記録される。

❌ E. find / -name core 2>&1 find.log

- 2>&1 find.log という記述は無効な構文。
- 正しい順番は > find.log 2>&1。

### まとめ

```
コマンド 説明 正誤
find / -name core > find.log 標準出力のみを保存（stderr は無視） ❌
find / -name core 2 >> find.log 標準エラーのみを追記（stdout は無視） ❌
`find / -name core 2 >& 1	find.log` 無効な構文
find / -name core > find.log 2>&1 stdout と stderr の両方を find.log に保存 ✅
find / -name core 2>&1 find.log 無効な構文 ❌
```

💡 ポイント

✅ 標準出力と標準エラーを同じファイルに保存するには > find.log 2>&1
✅ リダイレクトの順番が重要！ 2>&1 は > の後に書く！
❌ 無効な構文 (2>&1 find.log や | find.log) はエラーになる！

正解のコマンド

find / -name core > find.log 2>&1

## **PATH 変数にパスを追加する方法**

### **1. PATH 変数とは？**

`PATH` 変数は、**コマンドの検索パスを指定する環境変数** です。  
シェル（bash や zsh など）は、コマンドを実行するときに `PATH` 変数に設定されているディレクトリを順番に検索し、該当する実行ファイルを探します。

#### **現在の `PATH` 変数を確認**

```sh
echo $PATH
```

出力例:

```
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

このように :（コロン）で区切られたディレクトリが登録されています。

2. PATH にディレクトリを追加する

新しいパスを追加する方法は、次のように export コマンドを使います。

一時的に PATH にディレクトリを追加

export PATH=$PATH:/home/user/mybin

    -	$PATH（現在の PATH）の 末尾に :/home/user/mybin を追加
    -	export を使うことで、現在のシェル内で新しい PATH を適用

追加後の確認

echo $PATH

出力例

```
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/user/mybin
```

この方法は一時的 であり、シェルを閉じると元に戻ります。

3. PATH に永続的にパスを追加

シェルを閉じても PATH に新しいパスを追加した状態を維持するには、設定ファイルに記述 します。

---

方法①: ~/.bashrc に追加（bash の場合）

```
echo 'export PATH=$PATH:/home/user/mybin' >> ~/.bashrc
```

その後、変更を反映:

```
source ~/.bashrc
```

---

方法②: ~/.bash_profile に追加
~/.bash_profile は、ログインシェルでのみ適用されます。
もし ~/.bashrc ではなく ~/.bash_profile を使いたい場合:

```
echo 'export PATH=$PATH:/home/user/mybin' >> ~/.bash_profile
source ~/.bash_profile
```

---

方法③: ~/.zshrc に追加（zsh の場合）

zsh を使っている場合:

```
echo 'export PATH=$PATH:/home/user/mybin' >> ~/.zshrc
source ~/.zshrc
```

---

4. PATH に追加したディレクトリの優先度

PATH に追加する位置によって、実行されるコマンドの優先順位が変わります。

末尾に追加（低い優先度）

export PATH=$PATH:/home/user/mybin

- mybin にあるコマンドは、既存の /usr/bin などのコマンドより 後に検索 される。
- 既存のコマンドを上書きしない安全な方法。

先頭に追加（高い優先度）

export PATH=/home/user/mybin:$PATH

- mybin にあるコマンドが 最優先で実行 される。
- 例えば、/usr/bin/python より /home/user/mybin/python を優先的に使いたい場合に有効。
- 誤って重要なシステムコマンドを上書きするリスクがある ので注意。

---

5. PATH のリセット

もし PATH の設定を間違えたり、デフォルトに戻したい場合は、以下の方法を使います。

シェルを再起動

```
exec bash # bash の場合
exec zsh # zsh の場合
```

デフォルトの PATH にリセット

一時的にリセット:

```
export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
```

## または、~/.bashrc や ~/.zshrc を修正して source ~/.bashrc を実行。

💡 まとめ

```
方法 コマンド 効果
現在の PATH を確認 echo $PATH	現在の PATH を表示
一時的に追加	export PATH=$PATH:/home/user/mybin シェルを閉じるとリセット
永続的に追加（bash） echo 'export PATH=$PATH:/home/user/mybin' >> ~/.bashrc && source ~/.bashrc	シェル起動時に適用
永続的に追加（zsh）	echo 'export PATH=$PATH:/home/user/mybin' >> ~/.zshrc && source ~/.zshrc zsh 起動時に適用
先頭に追加（優先度高） export PATH=/home/user/mybin:$PATH /home/user/mybin のコマンドを最優先
デフォルトに戻す export PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin" PATH を初期状態にリセット
```

📝 PATH を追加する際の注意点

- ✅ 追加するディレクトリに 実行ファイルが含まれているか確認
- ✅ 先頭に追加すると優先度が変わるため注意（重要なコマンドを上書きするリスクあり）
- ✅ export PATH=$PATH:<追加するパス> の形式で設定する

この方法を使えば、PATH 変数を適切に管理できます！ 🚀

## **`lsmod` コマンドで表示されるモジュールの用途とは？**

### **1. `lsmod` コマンドとは？**

`lsmod` は、**カーネルモジュールの一覧を表示** するコマンドです。  
Linux のカーネルは、必要に応じて「カーネルモジュール（Kernel Modules）」をロードし、機能を拡張します。

#### **`lsmod` の基本的な使い方**

```sh
lsmod
```

出力例:

```
Module Size Used by
snd_hda_codec_realtek 90112 1
snd_hda_codec_generic 77824 1 snd_hda_codec_realtek
x86_pkg_temp_thermal 16384 0
intel_powerclamp 16384 0
snd_hda_intel 40960 2
```

2. lsmod の出力の見方

カラム 説明
Module モジュール名
Size モジュールのメモリサイズ（バイト単位）
Used by そのモジュールを使用している他のモジュール（数値は参照数）

例えば：

x86_pkg_temp_thermal 16384 0

- x86_pkg_temp_thermal → CPU の温度制御に関するモジュール
- 16384 バイト（約16KB）のメモリを使用
- 0 → 他のモジュールから参照されていない（単独で動作）

3. モジュールの用途を調べる方法

(1) modinfo で詳細情報を取得

各モジュールの詳細情報を確認するには modinfo コマンドを使用します。

modinfo x86_pkg_temp_thermal

出力例:

```
filename: /lib/modules/5.15.0-60-generic/kernel/drivers/thermal/x86_pkg_temp_thermal.ko
license: GPL
description: X86 Package Temperature Thermal Driver
author: Jacob Pan
```

ポイント

- description: → モジュールの説明
- filename: → モジュールの実際のパス

(2) lsmod | grep <モジュール名> で特定のモジュールを検索

lsmod | grep snd_hda

出力例:

```
snd_hda_codec_realtek 90112 1
snd_hda_codec_generic 77824 1 snd_hda_codec_realtek
snd_hda_intel 40960 2
```

オーディオ関連のモジュールがロードされていることが分かる。

4. よくあるカーネルモジュールと用途

モジュール名 用途
snd_hda_intel Intel HDA（High Definition Audio）ドライバ
x86_pkg_temp_thermal CPU の温度管理
nvidia NVIDIA の GPU ドライバ
usbcore USB デバイスの管理
ext4 ext4 ファイルシステムのサポート
i915 Intel 内蔵 GPU のドライバ
btusb Bluetooth USB デバイスのサポート

5. lsmod で表示された不要なモジュールを削除

カーネルモジュールは rmmod で削除可能（ただし、使用中のモジュールは削除不可）。

モジュールのアンロード

sudo rmmod <モジュール名>

例：

```
sudo rmmod x86_pkg_temp_thermal
```

モジュールを完全にブラックリスト化

不要なモジュールをロードされないようにするには、/etc/modprobe.d/blacklist.conf に追加：

echo "blacklist x86_pkg_temp_thermal" | sudo tee -a /etc/modprobe.d/blacklist.conf

その後、変更を適用：

sudo update-initramfs -u
sudo reboot

6. まとめ

```
✅ lsmod は、現在ロードされているカーネルモジュールを一覧表示するコマンド。
✅ 各モジュールの詳細は modinfo <モジュール名> で確認できる。
✅ lsmod | grep <キーワード> で特定のモジュールを検索可能。
✅ 不要なモジュールは rmmod で削除可能（ただし、依存関係に注意）。
✅ ブラックリスト設定 で永続的に無効化することもできる。
```

この知識を活用して、カーネルモジュールの管理を適切に行いましょう！ 🚀

## **RPM コマンドを使用してファイルのインストール元パッケージを表示する**

### **問題**

`rpm` コマンドを使用して、`/etc/yum.conf` ファイルのインストール元パッケージを表示したい。適切なコマンドを選択せよ。

### **正解**

✅ `rpm -qf /etc/yum.conf`  
✅ `rpm --query --file /etc/yum.conf`

---

### **解説**

RPM パッケージ管理システムでは、システム上のファイルがどのパッケージによって提供されているかを調べることができます。

#### **`-qf` または `--query --file` オプションの説明**

| コマンド                            | 説明                                                 |
| ----------------------------------- | ---------------------------------------------------- |
| `rpm -qf <ファイルパス>`            | 指定したファイルがどのパッケージに属しているかを表示 |
| `rpm --query --file <ファイルパス>` | `-qf` と同じ機能を持つ長い形式                       |

✅ 実行例:

```sh
rpm -qf /etc/yum.conf
```

出力例:

```
yum-4.2.23-3.el8.noarch
```

この出力から、/etc/yum.conf は yum パッケージによって提供されていることがわかります。

✅ --query --file 形式でも同様の結果が得られます。

rpm --query --file /etc/yum.conf

誤った選択肢の解説

コマンド 誤りの理由
rpm -ql /etc/yum.conf -ql はパッケージがインストールしたファイル一覧を表示するため、個別のファイルを指定するとエラーになる。
rpm -q /etc/yum.conf -q はパッケージ名を指定して情報を表示するため、ファイルを直接指定するとエラー。
rpm -qi /etc/yum.conf -qi はパッケージの詳細情報を表示するが、パッケージ名を直接指定する必要があるため、ファイルを指定するとエラー。

### まとめ

```
コマンド 説明 正誤
rpm -qf /etc/yum.conf 指定ファイルのインストール元パッケージを表示 ✅
rpm --query --file /etc/yum.conf -qf のロングオプション版 ✅
rpm -ql /etc/yum.conf ファイルのリストを表示するが、パッケージ名が必要 ❌
rpm -q /etc/yum.conf -q はパッケージ名を取るため、ファイル名指定は不可 ❌
rpm -qi /etc/yum.conf -qi はパッケージの詳細を表示するが、パッケージ名が必要 ❌
```

このように、-qf または --query --file を使うと、特定のファイルがどのパッケージに属しているのかを確認できます。

## **GPT（GUID Partition Table）の説明で正しいものはどれか？（3つ選択）**

### **問題**

次の選択肢のうち、GPT（GUID Partition Table）の説明として正しいものを3つ選べ。

### **正解**

✅ **A．EFI規格の中の機能の 1つである**  
✅ **D．ディスクには GUID が割り当てられる**  
✅ **E．パーティションには GUID が割り当てられる**

---

### **解説**

GPT（GUID Partition Table）は、従来のMBR（Master Boot Record）に代わる新しいパーティション方式で、**EFI（Extensible Firmware Interface）規格**の一部として定義されています。

#### **A．EFI 規格の中の機能の 1つである** ✅

- GPT は **UEFI（Unified Extensible Firmware Interface）** で使用されるパーティションテーブルの方式であり、EFI 規格の一部として定義されています。
- これにより、従来の MBR よりも多くのパーティションを扱うことが可能になります。

#### **D．ディスクには GUID が割り当てられる** ✅

- GPT では **ディスク全体に GUID（Globally Unique Identifier）** が割り当てられます。
- これにより、ディスクが一意に識別されるようになっています。

#### **E．パーティションには GUID が割り当てられる** ✅

- GPT では **各パーティションにも GUID が割り当てられます**。
- これにより、パーティションの種類（例: EFI システムパーティション、Linux ファイルシステムパーティションなど）を識別できるようになっています。

---

### **誤った選択肢の解説**

| 選択肢                                                                             | 誤りの理由                                                                                                                                                                         |
| ---------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **B．パーティション情報はディスクの先頭セクタに格納される** ❌                     | GPT では MBR のようにパーティション情報をディスクの**先頭セクタ**に格納せず、代わりに**ディスクの先頭と末尾の両方**にパーティション情報を持つ（バックアップ GPT ヘッダーがある）。 |
| **C．パーティションの開始と終了位置は CHS（Cylinder/Head/Sector）で指定される** ❌ | GPT では **CHS（Cylinder/Head/Sector）ではなく、LBA（Logical Block Addressing）** を使用してパーティションの開始・終了位置を指定する。                                             |

---

### **まとめ**

| 選択肢                                                                          | 説明                                                         | 正誤 |
| ------------------------------------------------------------------------------- | ------------------------------------------------------------ | ---- |
| **A．EFI 規格の中の機能の 1つである**                                           | GPT は EFI（UEFI）の一部として定義されている                 | ✅   |
| **B．パーティション情報はディスクの先頭セクタに格納される**                     | GPT ではディスクの先頭と末尾の両方にパーティション情報を持つ | ❌   |
| **C．パーティションの開始と終了位置は CHS（Cylinder/Head/Sector）で指定される** | GPT では LBA（Logical Block Addressing）を使用する           | ❌   |
| **D．ディスクには GUID が割り当てられる**                                       | GPT ではディスク全体に GUID を割り当てる                     | ✅   |
| **E．パーティションには GUID が割り当てられる**                                 | GPT では各パーティションにも GUID を割り当てる               | ✅   |

💡 **GPT は MBR に代わる最新のパーティションテーブルであり、EFI（UEFI）の標準仕様の一部として利用される。ディスク全体と各パーティションに GUID を割り当てることで、より多くのパーティションを管理し、CHS の制限を克服している。**

## **仮想化環境でクローンした仮想マシンの重複を避けるべき項目**

### **問題**

一つの仮想化ソフトウェア上で、同じ仮想マシンのクローンをいくつか動作させたい場合、重複してはならないものを **4つ** 選べ。

### **正解**

✅ **UUID**  
✅ **IPアドレス**  
✅ **SSHホスト鍵**  
✅ **マシンID**

---

### **解説**

仮想マシンのクローンを作成すると、元の仮想マシンと同じ設定がコピーされますが、以下の **4つの情報が重複すると問題が発生する** ため、変更する必要があります。

#### **1. UUID（Universally Unique Identifier）**

- **UUID は仮想マシンごとに異なる識別子** であり、仮想化ソフトウェアが VM を識別するために使用します。
- **UUID が重複すると、仮想化ソフトウェアが VM を適切に管理できなくなる可能性があります。**
- 仮想マシンの UUID は通常、仮想化ソフトウェア（例: VirtualBox, VMware）によって管理されます。
- **変更方法:**
  - VirtualBox の場合:
    ```sh
    VBoxManage modifyvm "VM_Name" --uuid <new_uuid>
    ```
  - `new_uuid` は `uuidgen` で生成可能:
    ```sh
    uuidgen
    ```

#### **2. IPアドレス**

- **同じネットワーク上で IP アドレスが重複すると、ネットワークの競合が発生し、通信できなくなる。**
- DHCP を使用している場合は、DHCP サーバーが異なる IP を割り当てるため、手動変更は不要なことが多い。
- **固定 IP の場合は、手動で IP アドレスを変更する必要がある。**
- **変更方法:**
  - `/etc/network/interfaces` または `/etc/netplan/` で IP 設定を変更（Linux）。
  - Windows では `ipconfig /release` → `ipconfig /renew` を実行。

#### **3. SSH ホスト鍵**

- **SSH ホスト鍵は、サーバーの正当性をクライアントが確認するための鍵情報。**
- 同じホスト鍵を持つサーバーが複数存在すると、**SSH 接続時に「MITM（中間者攻撃）の可能性がある」と警告が表示される**。
- **変更方法:**

```sh
 sudo rm -f /etc/ssh/ssh_host_*
 sudo dpkg-reconfigure openssh-server  # Debian系
 sudo systemctl restart sshd  # SSH サービスを再起動
```

4. マシンID
   - マシンID（/etc/machine-id）は、Linux システムが一意に識別されるための識別子。
   - マシンIDが重複すると、クラウドサービスや一部のアプリケーションで識別の問題が発生する。
   - 変更方法:

sudo rm -f /etc/machine-id
sudo systemd-machine-id-setup

誤った選択肢の解説

選択肢 誤りの理由
root ユーザのパスワード 仮想マシンごとに異なる方が望ましいが、システムの動作に直接影響はしない。
インストールされたパッケージ パッケージの構成が同じでも仮想マシンの識別には影響しないため、変更の必要はない。

### まとめ

```
重複すると問題が発生する項目（変更が必要） 変更不要な項目
✅ UUID（仮想マシンの識別子） ❌ root ユーザーのパスワード
✅ IPアドレス（ネットワークの競合防止） ❌ インストールされたパッケージ
✅ SSH ホスト鍵（セキュリティ問題防止）
✅ マシンID（システム識別の問題防止）
```

💡 仮想マシンのクローンを作成した後は、UUID、IPアドレス、SSHホスト鍵、マシンID を変更することで、正常に動作させることができます！

## **コンテナ型の仮想化の説明として正しいものはどれか（2つ選択）**

### **問題**

次の選択肢のうち、コンテナ型の仮想化に関する説明として正しいものを 2 つ選べ。

### **正解**

✅ **オーバーヘッドが少なく、リソース・構築・管理の面がシンプルである**  
✅ **Linuxカーネルの機能によってコンテナごとのユーザ管理やリソース制限ができる**

---

### **解説**

コンテナ型仮想化は、ホスト OS のカーネルを共有しながら、独立した環境を提供する技術です。代表的なコンテナ技術には **Docker, LXC, Podman** などがあります。

#### **1. オーバーヘッドが少なく、リソース・構築・管理の面がシンプルである** ✅

- **コンテナ型仮想化は、従来のハイパーバイザー型仮想化（Xen, KVM など）よりも軽量** です。
- ゲスト OS を必要とせず、ホスト OS のカーネルを直接利用するため、**メモリや CPU のオーバーヘッドが少ない**。
- コンテナは **イメージの構築・デプロイが容易で、管理がシンプル** である。

#### **2. Linuxカーネルの機能によってコンテナごとのユーザ管理やリソース制限ができる** ✅

- コンテナは **Linux のカーネル機能（cgroups, namespaces）を活用** して、ユーザ管理やリソース制限を行います。
- **cgroups（Control Groups）**:
  - CPU、メモリ、ディスク I/O などのリソース割り当てを制御。
- **namespaces**:
  - コンテナごとに分離された環境を提供（プロセス空間、ネットワーク空間、ユーザー空間など）。
- これにより、**コンテナ同士が干渉せず、安全な環境を構築できる**。

---

### **誤った選択肢の解説**

| **選択肢**                                                                              | **誤りの理由**                                                                                           |
| --------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------- |
| **コンテナ型ソフトウェアはXenやKVMである** ❌                                           | Xen や KVM は **ハイパーバイザー型仮想化** の技術であり、コンテナ型ではない。                            |
| **物理マシン上でハイパーバイザーを起動し、その上で仮想マシンとゲストOSを動作させる** ❌ | これは **ハイパーバイザー型仮想化の説明** であり、コンテナ型仮想化の特徴ではない。                       |
| **Linux上のコンテナでWindowsやmacOSを動作させることができる** ❌                        | コンテナは **ホスト OS のカーネルを共有する** ため、Linux のコンテナ上で Windows や macOS は動作しない。 |

---

### **まとめ**

| **正解（コンテナ型仮想化の特徴）**                      | **誤り（ハイパーバイザー型仮想化の特徴や誤解）**            |
| ------------------------------------------------------- | ----------------------------------------------------------- |
| ✅ **オーバーヘッドが少なく、管理がシンプル**           | ❌ Xen や KVM はコンテナ型ではなくハイパーバイザー型        |
| ✅ **Linuxカーネルの機能（cgroups, namespaces）を活用** | ❌ ハイパーバイザーを使用しないので、ゲストOSを動作させない |
|                                                         | ❌ Linux のコンテナ上で Windows や macOS は動作しない       |

💡 **コンテナ型仮想化は、ホスト OS のカーネルを共有しながら軽量な仮想環境を構築する技術であり、従来のハイパーバイザー型仮想化よりも高速かつ柔軟に運用できるのが特徴！**

## **IaaS で提供するリソースは次のうちどれか（3つ選択）**

### **問題**

次の選択肢のうち、IaaS（Infrastructure as a Service）で提供されるリソースとして正しいものを 3 つ選べ。

### **正解**

✅ **仮想マシン**  
✅ **仮想ネットワーク**  
✅ **ブロックストレージ**

---

### **解説**

IaaS（Infrastructure as a Service）は、クラウド上で **インフラストラクチャ（計算・ストレージ・ネットワーク）を提供するサービス** です。

ユーザーは、クラウドプロバイダーが提供する **仮想マシン、ストレージ、ネットワーク** などのリソースを利用して、自由にシステムを構築できます。

#### **1. 仮想マシン（Virtual Machine）** ✅

- **計算リソース（CPU, メモリ, OS）を仮想化して提供** するサービス。
- 例: **Amazon EC2（AWS）, Google Compute Engine（GCP）, Azure Virtual Machines（Azure）**
- ユーザーは、仮想マシン上でアプリケーションやデータベースを自由に構築・運用できる。

#### **2. 仮想ネットワーク（Virtual Network）** ✅

- **クラウド上で仮想的に構成されるネットワーク環境**。
- 例: **Amazon VPC（AWS）, Azure Virtual Network（Azure）**
- **ファイアウォールやルーティング、ロードバランサーを設定可能** で、仮想マシンやストレージとの接続を管理。

#### **3. ブロックストレージ（Block Storage）** ✅

- **仮想マシンのストレージとして使われるディスク型ストレージ**。
- 例: **Amazon EBS（AWS）, Google Persistent Disk（GCP）, Azure Managed Disks（Azure）**
- **データベースやOSディスクなどに適した高速ストレージ**。

---

### **誤った選択肢の解説**

| **選択肢**                          | **誤りの理由**                                                                                                              |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| **ソフトウェア** ❌                 | ソフトウェア（例: Office, SQL Server など）は **SaaS（Software as a Service）** に分類される。                              |
| **オブジェクトストレージ** ❌       | オブジェクトストレージ（Amazon S3, Google Cloud Storage など）は **PaaS（Platform as a Service）** で提供されることが多い。 |
| **ソフトウェアの開発、実行環境** ❌ | 開発・実行環境（例: AWS Lambda, Google App Engine など）は **PaaS** に分類される。                                          |

---

### **まとめ**

| **正解（IaaSの提供リソース）**         | **誤り（IaaSには含まれないリソース）**                   |
| -------------------------------------- | -------------------------------------------------------- |
| ✅ 仮想マシン（Virtual Machine）       | ❌ ソフトウェア（SaaS に分類される）                     |
| ✅ 仮想ネットワーク（Virtual Network） | ❌ オブジェクトストレージ（PaaS に分類されることが多い） |
| ✅ ブロックストレージ（Block Storage） | ❌ ソフトウェア開発・実行環境（PaaS に分類される）       |

💡 **IaaS は、クラウド上で「計算」「ネットワーク」「ストレージ」のインフラを提供するサービス。仮想マシン、仮想ネットワーク、ブロックストレージが主なリソース！**

## **IaaS で提供するリソースは次のうちどれか（3つ選択）**

### **問題**

次の選択肢のうち、IaaS（Infrastructure as a Service）で提供されるリソースとして正しいものを 3 つ選べ。

### **正解**

✅ **仮想マシン**  
✅ **仮想ネットワーク**  
✅ **ブロックストレージ**

---

### **解説**

IaaS（Infrastructure as a Service）は、クラウド上で **インフラストラクチャ（計算・ストレージ・ネットワーク）を提供するサービス** です。

ユーザーは、クラウドプロバイダーが提供する **仮想マシン、ストレージ、ネットワーク** などのリソースを利用して、自由にシステムを構築できます。

#### **1. 仮想マシン（Virtual Machine）** ✅

- **計算リソース（CPU, メモリ, OS）を仮想化して提供** するサービス。
- 例: **Amazon EC2（AWS）, Google Compute Engine（GCP）, Azure Virtual Machines（Azure）**
- ユーザーは、仮想マシン上でアプリケーションやデータベースを自由に構築・運用できる。

#### **2. 仮想ネットワーク（Virtual Network）** ✅

- **クラウド上で仮想的に構成されるネットワーク環境**。
- 例: **Amazon VPC（AWS）, Azure Virtual Network（Azure）**
- **ファイアウォールやルーティング、ロードバランサーを設定可能** で、仮想マシンやストレージとの接続を管理。

#### **3. ブロックストレージ（Block Storage）** ✅

- **仮想マシンのストレージとして使われるディスク型ストレージ**。
- 例: **Amazon EBS（AWS）, Google Persistent Disk（GCP）, Azure Managed Disks（Azure）**
- **データベースやOSディスクなどに適した高速ストレージ**。

---

### **誤った選択肢の解説**

| **選択肢**                          | **誤りの理由**                                                                                                              |
| ----------------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| **ソフトウェア** ❌                 | ソフトウェア（例: Office, SQL Server など）は **SaaS（Software as a Service）** に分類される。                              |
| **オブジェクトストレージ** ❌       | オブジェクトストレージ（Amazon S3, Google Cloud Storage など）は **PaaS（Platform as a Service）** で提供されることが多い。 |
| **ソフトウェアの開発、実行環境** ❌ | 開発・実行環境（例: AWS Lambda, Google App Engine など）は **PaaS** に分類される。                                          |

---

### **まとめ**

| **正解（IaaSの提供リソース）**         | **誤り（IaaSには含まれないリソース）**                   |
| -------------------------------------- | -------------------------------------------------------- |
| ✅ 仮想マシン（Virtual Machine）       | ❌ ソフトウェア（SaaS に分類される）                     |
| ✅ 仮想ネットワーク（Virtual Network） | ❌ オブジェクトストレージ（PaaS に分類されることが多い） |
| ✅ ブロックストレージ（Block Storage） | ❌ ソフトウェア開発・実行環境（PaaS に分類される）       |

💡 **IaaS は、クラウド上で「計算」「ネットワーク」「ストレージ」のインフラを提供するサービス。仮想マシン、仮想ネットワーク、ブロックストレージが主なリソース！**

## **クラウドにおけるサービスモデルのうち、ソフトウェアの開発・実行環境をサービスとして提供するものはどれか。**

### **問題**

次の選択肢のうち、ソフトウェアの **開発・実行環境をサービスとして提供** するものを選べ。

### **正解**

✅ **PaaS（Platform as a Service）**

---

### **解説**

クラウドコンピューティングには主に **3つのサービスモデル（IaaS, PaaS, SaaS）** があります。

#### **PaaS（Platform as a Service）とは？**

- **開発・実行環境を提供するクラウドサービス**。
- ユーザーは **アプリケーションの開発・デプロイに必要な環境をすぐに利用できる**。
- インフラ（サーバー・ネットワーク・OS）の管理が不要で、アプリケーション開発に集中できる。

**代表的な PaaS サービス**

- **Google App Engine（GCP）** - アプリケーションをデプロイして運用
- **AWS Elastic Beanstalk（AWS）** - 簡単に Web アプリをデプロイ
- **Azure App Services（Azure）** - クラウド上でアプリをホスティング

---

### **誤った選択肢の解説**

| **選択肢**                                 | **誤りの理由**                                                                                         |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------ |
| **IaaS（Infrastructure as a Service）** ❌ | 仮想マシン・ネットワーク・ストレージなどの **インフラ** を提供するサービス。開発環境の提供ではない。   |
| **オンプレミス（On-Premises）** ❌         | 自社のデータセンターやサーバーを使う **クラウドではない従来の方式**。                                  |
| **SaaS（Software as a Service）** ❌       | ユーザーが直接利用する **ソフトウェアそのもの** を提供する（例: Gmail, Google Docs）。                 |
| **HaaS（Hardware as a Service）** ❌       | 一般的なクラウドモデルではなく、**ハードウェア機能をリモートで提供する概念**（ほぼ使用されない用語）。 |

---

### **クラウドサービスの違い**

| **サービスモデル** | **提供内容**                         | **主な例**                                                   |
| ------------------ | ------------------------------------ | ------------------------------------------------------------ |
| **IaaS**           | 仮想マシン、ストレージ、ネットワーク | AWS EC2, Google Compute Engine, Azure VM                     |
| **PaaS**           | アプリ開発・実行環境                 | AWS Elastic Beanstalk, Google App Engine, Azure App Services |
| **SaaS**           | アプリケーションの提供               | Gmail, Google Drive, Microsoft 365                           |

💡 **PaaS は、開発者がアプリを簡単に構築・デプロイできる環境を提供するクラウドサービス！**

## **ハイパーバイザー型の仮想化の説明として正しいものはどれか（2つ選択）**

### **問題**

次の選択肢のうち、ハイパーバイザー型の仮想化の説明として正しいものを 2 つ選べ。

### **正解**

✅ **物理マシン上でハイパーバイザーを起動し、その上で仮想マシンとゲストOSを動作させる**  
✅ **ハイパーバイザーがサポートしていれば、動作させるゲストOSの種類に制限はない**

---

### **解説**

ハイパーバイザー型の仮想化は、物理マシン（ホスト）上で **ハイパーバイザー（Hypervisor）** を動作させ、その上で仮想マシン（VM）を管理する技術です。

ハイパーバイザーには **タイプ1（ベアメタル）** と **タイプ2（ホスト型）** の 2 種類があります。

#### **1. 物理マシン上でハイパーバイザーを起動し、その上で仮想マシンとゲストOSを動作させる** ✅

- **ハイパーバイザーは、物理マシンのリソースを管理し、複数の仮想マシンを作成できる。**
- ゲストOS は、仮想マシン上で独立して動作する。

**例:**

- **タイプ1（ベアメタル型）**
  - **VMware ESXi**
  - **Microsoft Hyper-V**
  - **KVM（Kernel-based Virtual Machine）**
- **タイプ2（ホスト型）**
  - **VirtualBox**
  - **VMware Workstation**

---

#### **2. ハイパーバイザーがサポートしていれば、動作させるゲストOSの種類に制限はない** ✅

- ハイパーバイザーが対応していれば、**Windows, Linux, macOS, BSD, Solaris など様々なOSを動作可能**。
- 例えば、**KVM は Linux だけでなく Windows も動作可能**。
- **VMware ESXi や VirtualBox では、Windows・Linux・macOS などが動作可能**。

---

### **誤った選択肢の解説**

| **選択肢**                                                       | **誤りの理由**                                                                          |
| ---------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **OSのリソースを「コンテナ」という単位で隔離して共有する** ❌    | これは **コンテナ型仮想化（LXC, Docker）** の説明であり、ハイパーバイザー型とは異なる。 |
| **ハイパーバイザー型の仮想化ソフトウェアはLXCやDockerである** ❌ | LXC や Docker は **コンテナ型仮想化** であり、ハイパーバイザーではない。                |
| **ゲストOSはLinuxしか使用できない** ❌                           | ハイパーバイザーが対応していれば、Windows・macOS など **複数のOSを動作可能**。          |

---

### **ハイパーバイザー型 vs コンテナ型 の違い**

| **項目**             | **ハイパーバイザー型仮想化**               | **コンテナ型仮想化**                       |
| -------------------- | ------------------------------------------ | ------------------------------------------ |
| **主なソフトウェア** | VMware ESXi, KVM, VirtualBox, Hyper-V      | Docker, LXC, Podman                        |
| **動作するOS**       | Windows, Linux, macOS, BSD など            | Linux のカーネルを共有（他OSは不可）       |
| **リソース管理**     | 物理マシンのリソースを仮想マシン単位で分割 | 1つのOSを複数のコンテナで共有              |
| **仮想環境の独立性** | ゲストOSごとに完全に独立                   | カーネルを共有するため、完全には独立しない |
| **起動速度**         | OS の起動が必要なため遅め                  | ホストOS上で動作するため高速               |

---

### **まとめ**

| **正解（ハイパーバイザー型の説明）**                                                |
| ----------------------------------------------------------------------------------- |
| ✅ 物理マシン上でハイパーバイザーを起動し、その上で仮想マシンとゲストOSを動作させる |
| ✅ ハイパーバイザーがサポートしていれば、動作させるゲストOSの種類に制限はない       |

💡 **ハイパーバイザー型仮想化は、仮想マシンごとにOSを完全に分離できる。対応していれば、Linux 以外のOSも動作可能！**

## **クラウドで提供する仮想化環境について正しい説明はどれか（3つ選択）**

### **問題**

次の選択肢のうち、クラウドで提供する仮想化環境について正しいものを 3 つ選べ。

### **正解**

✅ **仮想マシンのことをインスタンスと呼ぶ**  
✅ **仮想マシンへのOSのインストールはテンプレートを利用できる**  
✅ **ブログサービス環境などのように、ユーザの用途に応じて利用可能なコンテナをアプリケーションコンテナと呼ぶ**

---

### **解説**

クラウド環境では、仮想化技術を利用して **仮想マシン（VM）やコンテナ** を提供します。主に **IaaS（Infrastructure as a Service）** や **PaaS（Platform as a Service）** のサービス形態で活用されます。

#### **1. 仮想マシンのことをインスタンスと呼ぶ** ✅

- クラウドサービス（AWS, GCP, Azure など）では、**仮想マシン（VM）を「インスタンス」** と呼ぶ。
- 例: **AWS EC2 インスタンス, GCP Compute Engine インスタンス**
- **物理マシンではなく、仮想的に作成されるサーバーを指す。**

#### **2. 仮想マシンへのOSのインストールはテンプレートを利用できる** ✅

- クラウドでは **OSのインストールを手動で行うのではなく、事前に用意されたテンプレート（イメージ）を使用** する。
- 例: **AWS AMI（Amazon Machine Image）, GCPのイメージ, OpenStackのGlance**
- **Ubuntu, CentOS, Windows Server などのOSイメージを選択して、すぐに仮想マシンを作成できる。**

#### **3. ブログサービス環境などのように、ユーザの用途に応じて利用可能なコンテナをアプリケーションコンテナと呼ぶ** ✅

- **アプリケーションコンテナとは、特定のアプリケーションを実行するためのコンテナ。**
- 例: **WordPress, MySQL, Nginx, Redis のようなコンテナがある**
- **Docker や Kubernetes などのコンテナ技術を活用し、ブログサービスやウェブアプリの実行環境を提供する。**
- **PaaS（Platform as a Service）では、アプリケーションコンテナが一般的に利用される。**

---

### **誤った選択肢の解説**

| **選択肢**                                          | **誤りの理由**                                                                                                                        |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| **仮想ネットワークのことをインスタンスと呼ぶ** ❌   | **インスタンスとは仮想マシン（VM）のこと** であり、仮想ネットワークは **VPC（Virtual Private Cloud）** や **Subnet** などと呼ばれる。 |
| **クラウドではコンテナ型の仮想化は利用できない** ❌ | クラウドでは **コンテナ型の仮想化も利用可能**（例: AWS ECS, AWS Fargate, GCP Cloud Run, Azure AKS など）。                            |

---

### **クラウドにおける仮想化技術の種類**

| **種類**             | **説明**                                       | **代表的なサービス**                      |
| -------------------- | ---------------------------------------------- | ----------------------------------------- |
| **仮想マシン（VM）** | OSごとに仮想化された環境を提供                 | AWS EC2, GCP Compute Engine, Azure VM     |
| **コンテナ型仮想化** | ホストOSを共有し、アプリケーション単位で仮想化 | AWS ECS/Fargate, GCP Cloud Run, Azure AKS |
| **仮想ネットワーク** | クラウド上で仮想的なネットワークを構築         | AWS VPC, GCP VPC, Azure Virtual Network   |

---

### **まとめ**

| **正解（クラウドの仮想化環境に関する説明）**                                                              |
| --------------------------------------------------------------------------------------------------------- |
| ✅ 仮想マシンのことをインスタンスと呼ぶ                                                                   |
| ✅ 仮想マシンへのOSのインストールはテンプレートを利用できる                                               |
| ✅ ブログサービス環境などのように、ユーザの用途に応じて利用可能なコンテナをアプリケーションコンテナと呼ぶ |

💡 **クラウド環境では、仮想マシン（インスタンス）とコンテナを活用することで、効率的にシステムを構築できる！**

## **クラウドにおけるサービスモデルのうち、ソフトウェアの開発・実行環境をサービスとして提供するものはどれか**

### **問題**

次の選択肢のうち、**ソフトウェアの開発・実行環境** をサービスとして提供するものを選べ。

### **選択肢**

- SaaS
- オンプレミス
- IaaS
- HaaS
- PaaS

### **正解**

✅ **PaaS（Platform as a Service）**

---

### **解説**

クラウドサービスには、主に以下の **3 つのモデル（IaaS / PaaS / SaaS）** があります。

| **サービスモデル**                      | **提供されるリソース**                                               | **ユーザーの管理範囲**                      | **代表的なサービス**                                     |
| --------------------------------------- | -------------------------------------------------------------------- | ------------------------------------------- | -------------------------------------------------------- |
| **IaaS（Infrastructure as a Service）** | **仮想マシン, ストレージ, ネットワーク**                             | OS やアプリケーションの管理はユーザーが行う | AWS EC2, GCP Compute Engine, Azure VM                    |
| **PaaS（Platform as a Service）**       | **アプリケーションの開発・実行環境（OS, ミドルウェア, ランタイム）** | アプリケーション開発のみをユーザーが管理    | AWS Elastic Beanstalk, GCP App Engine, Azure App Service |
| **SaaS（Software as a Service）**       | **アプリケーションそのものを提供**                                   | ユーザーはソフトウェアを利用するだけ        | Google Workspace, Microsoft 365, Salesforce              |

---

### **PaaS（Platform as a Service）とは？**

✅ **開発者向けに、アプリケーションの開発・実行環境を提供するクラウドサービス。**  
✅ **サーバーや OS の管理は不要** で、アプリ開発に集中できる。  
✅ **開発に必要なツール（DB・フレームワーク・言語環境）もクラウド側が提供。**

📌 **PaaSの具体例**

- **AWS Elastic Beanstalk**（AWS の PaaS サービス）
- **Google App Engine（GCP）**
- **Microsoft Azure App Service**
- **Heroku**

📌 **PaaS のメリット**

- **サーバー管理不要**（IaaS と違い、OS やミドルウェアの管理を気にしなくて良い）
- **開発に集中できる**（ランタイム環境・DB・フレームワークが用意されている）
- **スケーリングが容易**（クラウド側がリソースを自動で拡張）

---

### **誤った選択肢の解説**

| **選択肢**                                 | **誤りの理由**                                                                                        |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------- |
| **SaaS（Software as a Service）** ❌       | 完成したアプリケーション（例: Google Drive, Microsoft 365）を提供するモデルで、開発環境は含まれない。 |
| **オンプレミス（On-Premise）** ❌          | クラウドではなく、**企業が独自にインフラを管理** する方式。                                           |
| **IaaS（Infrastructure as a Service）** ❌ | **仮想マシン・ネットワーク・ストレージ** を提供するが、アプリの開発環境は含まれない。                 |
| **HaaS（Hardware as a Service）** ❌       | 一般的なクラウドモデルには含まれない（物理ハードウェアを貸し出すサービスのこと）。                    |

---

### **まとめ**

✅ **PaaS（Platform as a Service）** は、**アプリ開発のためのプラットフォームを提供するクラウドサービス。**  
✅ サーバー・OS・ミドルウェアの管理は不要で、開発者はアプリケーションの開発に専念できる。  
✅ **代表例: AWS Elastic Beanstalk, Google App Engine, Azure App Service, Heroku**

| **サービスモデル** | **主な用途**                   | **代表的なサービス**                     |
| ------------------ | ------------------------------ | ---------------------------------------- |
| **IaaS**           | 仮想マシン、ネットワークの提供 | AWS EC2, GCP Compute Engine              |
| **PaaS**           | 開発・実行環境の提供           | AWS Elastic Beanstalk, Google App Engine |
| **SaaS**           | アプリケーションの提供         | Google Drive, Microsoft 365              |

💡 **PaaS を活用すると、インフラ管理不要でアプリ開発をスピーディに進められる！**

## **RPM コマンドを使用してインストール前のパッケージの依存関係を調べる**

### **問題**

次の選択肢のうち、**インストール前の「emacs-23.1-28.el6.x86_64.rpm」パッケージの依存関係を調べる** ために使用できるコマンドを選べ。（2つ選択）

### **選択肢**

- `rpm -qRp emacs-23.1-28.el6.x86_64.rpm`
- `rpm -qDp emacs-23.1-28.el6.x86_64.rpm`
- `rpm --query --depends --package emacs-23.1-28.el6.x86_64.rpm`
- `rpm --query --requires --package emacs-23.1-28.el6.x86_64.rpm`
- `rpm -qlp emacs-23.1-28.el6.x86_64.rpm`

### **正解**

✅ `rpm -qRp emacs-23.1-28.el6.x86_64.rpm`  
✅ `rpm --query --requires --package emacs-23.1-28.el6.x86_64.rpm`

---

### **解説**

`rpm` コマンドは、RPM パッケージの管理に使用されるコマンドで、**パッケージの情報の取得・インストール・削除** などを行うことができます。

パッケージの **依存関係（requirements）** を調べるには、以下のオプションを使用します。

| **コマンド**                                     | **説明**                                          |
| ------------------------------------------------ | ------------------------------------------------- |
| `rpm -qR <パッケージ名>`                         | インストール済みのパッケージの依存関係を調べる    |
| `rpm -qRp <RPMファイル>`                         | **インストール前のパッケージ** の依存関係を調べる |
| `rpm --query --requires --package <RPMファイル>` | `-qRp` と同じ。依存関係を表示                     |

`rpm -qRp` は、指定した **RPM ファイル** に必要な依存関係を表示するオプションです。

### **コマンドの実行例**

#### `rpm -qRp`

```sh
$ rpm -qRp emacs-23.1-28.el6.x86_64.rpm
/bin/sh
/bin/rm
libX11.so.6
libc.so.6
libgcc_s.so.1
```

このように、emacs の動作に必要なライブラリが表示されます。

rpm --query --requires --package

$ rpm --query --requires --package emacs-23.1-28.el6.x86_64.rpm
/bin/sh
/bin/rm
libX11.so.6
libc.so.6
libgcc_s.so.1

-qRp と --query --requires --package は同じ結果を出力します。

### 不正解の選択肢の解説

### 選択肢 誤りの理由

rpm -qDp emacs-23.1-28.el6.x86_64.rpm ❌ -qDp は無効なオプション
rpm --query --depends --package emacs-23.1-28.el6.x86_64.rpm ❌ --depends というオプションは存在しない（--requires が正しい）
rpm -qlp emacs-23.1-28.el6.x86_64.rpm ❌ -qlp は パッケージに含まれるファイル一覧 を表示する（依存関係ではない）

### まとめ

✅ RPM パッケージの依存関係を調べるには

```
rpm -qRp <RPMファイル>
rpm --query --requires --package <RPMファイル>
```

✅ -qRp または --query --requires --package を使用することで、インストール前 のパッケージの依存関係を確認できる。

💡 ポイント

- -qR → インストール済み のパッケージの依存関係
- -qRp → インストール前（RPMファイル） の依存関係
- -qlp はパッケージに含まれるファイルの一覧を表示する

✅ よって、正解は rpm -qRp と rpm --query --requires --package！

## システム起動に必要なファイルが格納されるディレクトリはどれか？

### 問題

Linuxカーネルなど、**システムを起動するために必須のファイル**が格納されるディレクトリは次のうちどれか。

---

### 選択肢

- A. `/etc`
- B. `/boot`
- C. `/sbin`
- D. `/dev`
- E. `/bin`

---

### 正解

✅ **B. `/boot`**

---

### 解説

| ディレクトリ | 役割                                                                                                                                                                     |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `/boot`      | Linuxカーネル（`vmlinuz`）、初期RAMディスク（`initrd` または `initramfs`）、ブートローダ（GRUB）の設定ファイルなど、**起動に必要なファイル**を格納する重要なディレクトリ |
| `/etc`       | 設定ファイルを格納（例：`/etc/fstab`, `/etc/hostname` など）                                                                                                             |
| `/sbin`      | システム管理用のコマンドを格納（`mount`, `reboot`, `ifconfig` など）                                                                                                     |
| `/dev`       | デバイスファイルを格納（仮想ファイル、例：`/dev/sda`, `/dev/null`）                                                                                                      |
| `/bin`       | 一般ユーザー・管理者が共通で使う基本コマンド（`ls`, `cp`, `mv` など）を格納                                                                                              |

---

### まとめ

- Linuxカーネル・ブートローダ・初期RAMディスク → **`/boot`**
- 設定ファイル → `/etc`
- デバイスファイル → `/dev`
- システムコマンド → `/sbin`, `/bin`

```bash
ls /boot
```

## Linuxをインストールする際、ルートパーティションから分割できないディレクトリはどれか？（全て選択）

### 問題

Linuxをインストールする際、**ルートパーティション（`/`）から分割できないディレクトリ**は次のうちどれか。（全て選べ）

---

### 選択肢

- `/home`
- `/dev`
- `/sbin`
- `/lib`
- `/usr`

---

### 正解

✅ **/lib**  
✅ **/dev**  
✅ **/sbin**

---

### 解説

| ディレクトリ | 分割の可否 | 解説                                                                                                             |
| ------------ | ---------- | ---------------------------------------------------------------------------------------------------------------- |
| `/lib`       | ❌不可     | 起動時に必要な共有ライブラリ（`/sbin` や `/bin` にあるコマンドが依存）を格納しており、ルートパーティションに必須 |
| `/dev`       | ❌不可     | デバイスファイル（例：`/dev/sda`）が格納され、ブートプロセスで必要                                               |
| `/sbin`      | ❌不可     | システム管理用のコマンド（`fsck`, `init` など）があり、起動時に必要                                              |
| `/home`      | ✅分割可   | ユーザーのホームディレクトリ。別パーティションや別ディスクにも分けられる                                         |
| `/usr`       | ✅分割可   | 一般ユーザー向けアプリケーションやライブラリを格納。起動後にマウントしても問題ないように設計されている           |

---

### まとめ

- 起動時に**必要不可欠なディレクトリ（分割不可）**：
  - `/lib`
  - `/dev`
  - `/sbin`
- 起動後でも利用可能なディレクトリ（分割可能）：
  - `/home`
  - `/usr`

```bash
ls /lib /dev /sbin
```

## Linuxシステムを構築するに当たって、推奨構成として必要なパーティションは次のうちどれか？（2つ選択）

### 問題

Linuxシステムを構築するに当たって、**推奨構成として必要なパーティション**は次のうちどれか。（2つ選べ）

---

### 選択肢

- スワップ領域
- `/sbin`
- `/bin`
- `/boot`
- ルートパーティション

---

### 正解

✅ **ルートパーティション**  
✅ **スワップ領域**

---

### 解説

| 項目                     | パーティションとして必要か | 解説                                                       |
| ------------------------ | -------------------------- | ---------------------------------------------------------- |
| ルートパーティション `/` | ✅ 必須                    | システム全体の基盤となるパーティション。最も重要           |
| スワップ領域             | ✅ 推奨                    | 物理メモリが不足したときにディスク上でメモリを補う役割     |
| `/sbin`                  | ❌ 不要                    | `/` に含まれるディレクトリであり、個別パーティションは不要 |
| `/bin`                   | ❌ 不要                    | 同上。起動に必要なコマンドは `/` 配下に存在                |
| `/boot`                  | ❌ 必須ではない            | 起動専用に分けることもあるが、必須構成ではない             |

---

### まとめ

- **ルートパーティション**：すべての基本ファイルが格納される中心的な領域
- **スワップ領域**：物理メモリの補助として使用される
- `/boot` などは環境に応じて分けることもあるが、**必須ではない**

```bash
lsblk
```

## Linuxをインストールする際、ルートパーティションとは別のパーティションを割り当てることが可能なディレクトリはどれか？（全て選択）

### 問題

Linuxをインストールする際、**ルートパーティションとは別のパーティションを割り当てることが可能なディレクトリ**は次のうちどれか。（全て選べ）

---

### 選択肢

- `/boot`
- `/tmp`
- `/bin`
- `/etc`
- `/sbin`

---

### 正解

✅ **/boot**  
✅ **/tmp**

---

### 解説

| ディレクトリ | 分割の可否 | 解説                                                                                   |
| ------------ | ---------- | -------------------------------------------------------------------------------------- |
| `/boot`      | ✅ 可能    | ブートローダやカーネル関連のファイルを格納。分割することでルートが壊れても起動を保てる |
| `/tmp`       | ✅ 可能    | 一時ファイル保存用ディレクトリ。独立させて容量管理しやすくすることがある               |
| `/bin`       | ❌ 不可    | 起動に必要な基本コマンドを含むため、ルートに含める必要あり                             |
| `/etc`       | ❌ 不可    | システム設定ファイルを含むため、ルートに必要                                           |
| `/sbin`      | ❌ 不可    | システム管理用コマンドがあり、起動に必要なためルートに含める必要がある                 |

---

### まとめ

- **別パーティションに分割可能なディレクトリ**：
  - `/boot`：起動関連ファイルを独立して管理できる
  - `/tmp`：一時ファイル用で消えても問題ないため、分離可能
- **分割不可のディレクトリ**（起動に必須）：
  - `/bin`, `/etc`, `/sbin`

```bash
df -h
```

## LVMの説明として正しいものはどれか？（4つ選択）

### 問題

LVM（Logical Volume Manager）の説明として**正しいもの**は次のうちどれか。（4つ選べ）

---

### 選択肢

- 論理ボリュームと物理ボリュームの間には、一対一対応の関係がある
- ボリュームグループに対し、後から物理ボリュームを加えたり、削除したりできる
- ボリュームグループは、物理ボリュームを集めて構成された仮想的な領域である
- 論理ボリュームを動的にリサイズすることができる
- スナップショットを取得することができる
- ファイルシステムを自動的に作成することができる

---

### 正解

✅ **論理ボリュームを動的にリサイズすることができる**  
✅ **ボリュームグループは、物理ボリュームを集めて構成された仮想的な領域である**  
✅ **ボリュームグループに対し、後から物理ボリュームを加えたり、削除したりできる**  
✅ **スナップショットを取得することができる**

---

### 解説

| 選択肢                                                                     | 正誤 | 解説                                                                                                           |
| -------------------------------------------------------------------------- | ---- | -------------------------------------------------------------------------------------------------------------- |
| 論理ボリュームと物理ボリュームの間には、一対一対応の関係がある             | ❌   | 論理ボリュームは物理ボリュームをまたいで構成可能であり、一対多の関係になる                                     |
| ボリュームグループに対し、後から物理ボリュームを加えたり、削除したりできる | ✅   | 柔軟なディスク管理が可能                                                                                       |
| ボリュームグループは、物理ボリュームを集めて構成された仮想的な領域である   | ✅   | LVMの中核的な概念                                                                                              |
| 論理ボリュームを動的にリサイズすることができる                             | ✅   | ファイルシステムによって制限はあるが、拡張・縮小が可能                                                         |
| スナップショットを取得することができる                                     | ✅   | バックアップ用途などで活用される                                                                               |
| ファイルシステムを自動的に作成することができる                             | ❌   | LVMはパーティション・ボリューム管理の仕組みであり、ファイルシステムは別途作成する必要がある（例：`mkfs.ext4`） |

---

### まとめ

- **LVMは柔軟なディスク管理を可能にする仕組み**
  - 論理ボリュームの拡張・縮小
  - スナップショットの取得
  - 動的な構成変更（PVの追加/削除）

```bash
lvextend -L +5G /dev/vg0/lv0  # 例：論理ボリュームの拡張
lvcreate -s -n snap0 -L 1G /dev/vg0/lv0  # スナップショットの作成
```

## パーティションの設計について適切なものはどれか？

### 問題

パーティションの設計について、**適切なもの**は次のうちどれか。

---

### 選択肢

- スワップ領域の名前は `/swapfile` にしなければならない
- `/etc` はルートパーティション（`/`）とは別のディスクに割り当てる
- `/boot` は必ず RAID 上に構成する
- `/var` は高速に書き込みできるディスクに割り当てる

---

### 正解

✅ **/var は高速に書き込みできるディスクに割り当てる**

---

### 解説

| 選択肢                                                    | 正誤 | 解説                                                                                                    |
| --------------------------------------------------------- | ---- | ------------------------------------------------------------------------------------------------------- |
| スワップ領域の名前は `/swapfile` にしなければならない     | ❌   | スワップ領域はスワップファイルまたはパーティションで設定でき、名前は任意（`/swapfile` は一例）          |
| `/etc` はルートパーティションとは別のディスクに割り当てる | ❌   | `/etc` はシステム設定ファイルを含むため、通常は `/` パーティションと同じにする                          |
| `/boot` は必ず RAID 上に構成する                          | ❌   | 必須ではない。ブート環境によってはRAIDを避けることもある                                                |
| `/var` は高速に書き込みできるディスクに割り当てる         | ✅   | `/var` はログやメール、スプールなど書き込みが頻繁に行われるため、高速なディスクに割り当てるのが望ましい |

---

### まとめ

- `/var` はログファイルやメール、キャッシュなどの頻繁な書き込みが発生する  
  → **高速ディスクに割り当てるのがベスト**
- `/etc` や `/boot` については特殊な環境を除き、基本的に `/` と同じディスク上で問題なし
- スワップファイルの名前は**柔軟に決められる**

```bash
df -h /var
```

## システムの起動には必須でないプログラムやライブラリが格納されたディレクトリはどれか？

### 問題

システムの**起動には必須でない**プログラムやライブラリが格納されたディレクトリは次のうちどれか。

---

### 選択肢

- `/sbin`
- `/usr`
- `/bin`
- `/etc`
- `/dev`

---

### 正解

✅ **/usr**

---

### 解説

| ディレクトリ | 起動に必要か | 解説                                                                     |
| ------------ | ------------ | ------------------------------------------------------------------------ |
| `/sbin`      | ✅ 必要      | システム管理に使うコマンド（`fsck`, `reboot` など）を含むため起動に必須  |
| `/usr`       | ❌ 不要      | ユーザー向けアプリケーションやライブラリが含まれ、起動後に必要           |
| `/bin`       | ✅ 必要      | 基本的なコマンド（`ls`, `cp`, `mv` など）を含むため起動に必要            |
| `/etc`       | ✅ 必要      | 設定ファイル（`fstab`, `hostname` など）が含まれるため起動に必要         |
| `/dev`       | ✅ 必要      | デバイスファイル（`/dev/sda`, `/dev/null` など）が含まれるため起動に必要 |

---

### まとめ

- `/usr` は**起動後**に必要となるライブラリやコマンドが主に配置されている
- 起動に必須のディレクトリは `/bin`, `/sbin`, `/etc`, `/dev` など
- `/usr` は分離パーティションにすることも可能だが、マウントタイミングに注意

```bash
ls /usr/bin
```

## 論理ボリュームを作成するまでの手順として正しいものはどれか？

### 問題

以下のコマンド順のうち、**論理ボリューム（Logical Volume）を作成するまでの正しい手順**として適切なものはどれか。選びなさい。

---

### 選択肢

- `vgcreate`, `lvcreate`, `pvcreate`
- `lvcreate`, `pvcreate`, `vgcreate`
- `vgcreate`, `pvcreate`, `lvcreate`
- `pvcreate`, `lvcreate`, `vgcreate`
- `pvcreate`, `vgcreate`, `lvcreate`
- `lvcreate`, `vgcreate`, `pvcreate`

---

### 正解

✅ **pvcreate, vgcreate, lvcreate**

---

### 解説

| コマンド   | 役割                                                                            |
| ---------- | ------------------------------------------------------------------------------- |
| `pvcreate` | 物理ボリューム（Physical Volume）を初期化。LVMで使えるようにする                |
| `vgcreate` | ボリュームグループ（Volume Group）を作成し、1つ以上の物理ボリュームを割り当てる |
| `lvcreate` | 論理ボリューム（Logical Volume）を作成。利用可能なボリュームグループの中に作る  |

LVM構成の流れ：

```text
物理ディスク → PV（物理ボリューム） → VG（ボリュームグループ） → LV（論理ボリューム）
```
