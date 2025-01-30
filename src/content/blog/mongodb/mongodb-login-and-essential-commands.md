---
author: Taro Gray
pubDatetime: 2024-11-10T11:00:00.00Z
title: "MongoDBのログイン方法と実務で役立つコマンド一覧"
postSlug: mongodb-login-and-essential-commands
featured: true
draft: false
ogImage: "https://example.com/path/to/image.jpg" # 任意のURLに置き換えてください
tags:
  - MongoDB
  - Database
  - CLI
description: "MongoDBのログイン方法と、データベース管理において便利なコマンドの一覧を紹介します。初心者から実務で利用できるコマンドをまとめました。"
---

## Table of Contents

## Introduction

MongoDBは、NoSQLデータベースとして広く利用されており、CLIからの操作がとても便利です。この記事では、MongoDBバージョン6以降で利用するmongoshを使ったログイン方法と、業務で活用できるMongoDBのコマンドを一通り紹介します。

## MongoDBへのログイン方法

MongoDBにCLIからログインするには、以下のコマンドを使用します。バージョン6からは従来のmongoコマンドに代わり、mongoshが使われるようになりました。

mongosh <DB名> -u <ユーザ名> -p <パスワード>

このコマンドで、指定したデータベースにログインできます。また、指定したユーザー名とパスワードで認証を行い、安全にアクセスできます。

実務で役立つMongoDBコマンド

以下は、データベースやコレクションの操作、データの検索、インデックス管理など、実務で役立つMongoDBコマンドの一覧です。

## データベース操作

    •	DB一覧表示

show dbs

    •	使用DBの切り替え

use <データベース名>

    •	選択中のDBの確認

db.stats()

    •	DB作成（1件でもコレクションを作成しないと表示されない）

use <データベース名>

    •	DB削除（選択中のDBが削除される）

db.dropDatabase()

## コレクション操作

    •	コレクション一覧

show collections

    •	コレクション作成

db.createCollection('collection_name')

    •	コレクション削除

db.<コレクション名>.drop()

## ドキュメント検索

    •	ドキュメント一覧（全件）

db.<コレクション名>.find()

    •	整形して表示

db.<コレクション名>.find().pretty()

    •	AND条件検索

db.<コレクション名>.find({column1: 'aaa', column2: 10})

    •	OR条件検索

db.<コレクション名>.find({column_name1: 'aaa'}, {column_name2: 10})

    •	否定条件検索

db.<コレクション名>.find({column_name: {$ne: 'aaa'}})

    •	大小比較検索
    •	「xxxより大きい」条件

db.<コレクション名>.find({column_name: {$gt: 10}})

    •	「xxx以下」条件

db.<コレクション名>.find({column_name: {$lte: 10}})

    •	正規表現で検索

db.<コレクション名>.find({column_name: /^aaa/})

## インデックスの管理

    •	インデックス作成

db.<コレクション名>.createIndex({column_name: 1})

    •	名前付きインデックス作成

db.<コレクション名>.createIndex({column_name: 1}, {name: 'index_name'})

    •	インデックス削除

db.<コレクション名>.dropIndex('index_name')

    •	ユニーク（一意）制約付きインデックス

db.<コレクション名>.createIndex({column: 1}, {unique: true, sparse: true})

## Conclusion

MongoDBでよく使う基本的なコマンドをまとめました。データベースやコレクションの操作、ドキュメント検索やインデックス管理など、実務で便利なコマンドを覚えておくことで、MongoDBの利用効率が大幅に向上します。
