---
author: Taro Gray
pubDatetime: 2023-11-28T09:46:00.000Z
title: 【Linuxコマンドマスターシリーズ】ファイルパーミッションとスーパーユーザーのマスター
postSlug: linux-filePermission-groups-chomod-su
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
description: Linuxシステムにおいて、ファイルパーミッションとスーパーユーザーの操作は重要な役割を果たします。これらを理解し適切に使用することで、システムのセキュリティを保ちつつ、効率的な管理が可能になります。
---

## Table of contents

## Linuxファイルパーミッションとスーパーユーザーのマスター

Linuxシステムにおいて、ファイルパーミッションとスーパーユーザーの操作は重要な役割を果たします。これらを理解し適切に使用することで、システムのセキュリティを保ちつつ、効率的な管理が可能になります。

## ファイルの所有者とグループ

Linuxでは、各ファイルには所有者（オーナー）とグループが設定されています。

### ls -l コマンド

`ls -l` コマンドを使用して、ファイルの詳細な情報を表示します。これには、所有者とグループも含まれます。

```bash
# ファイルの詳細情報を表示
ls -l filename.txt
```

### groups コマンド

`groups` コマンドを使うと、現在ログインしているユーザーが所属するグループを表示できます。

```bash
# 所属グループを表示
groups
```

## ファイルパーミッション

ファイルには、読み取り（r）、書き込み（w）、実行（x）の3種類のパーミッションが設定されています。

### chmod コマンド

`chmod` コマンドを使用して、ファイルのパーミッションを変更します。

```bash
# ファイルに実行権限を追加（所有者のみ）
chmod u+x filename.txt

# グループに読み取り権限を追加
chmod g+r filename.txt

# 他のユーザーの書き込み権限を削除
chmod o-w filename.txt
```

## スーパーユーザー su

`su` コマンドは、スーパーユーザーや他のユーザーとしてシェルにログインするために使用されます。

```bash
# スーパーユーザーに切り替え
su
```

## ハッカーの小技：システム管理

ハッカーは、システムの脆弱性を探る際にこれらのコマンドを使います。例えば、不適切に設定されたファイルパーミッションを利用してシステムにアクセスすることがあります。また、`su` コマンドを使って特権昇格を試みることもあります。

## まとめ

ファイルパーミッションの理解と適切な設定、スーパーユーザーとしての効果的な操作は、Linuxシステムを安全かつ効率的に管理するために不可欠です。これらのコマンドを適切に使用することで、システムのセキュリティと整合性を維持することができます。この記事では、Linuxのファイルパーミッションの設定とスーパーユーザーとしての操作に焦点を当てました。これにより、読者はシステムの管理とセキュリティ向上に役立つ知識を得ることができます。