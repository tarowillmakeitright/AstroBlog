---
author: Taro Gray
pubDatetime: 2024-11-10T14:00:00.00Z
title: "MongoDBへのJSONデータインポート方法 - mongoimportコマンドの使い方"
postSlug: mongodb-json-import-mongoimport
featured: true
draft: false
tags:
  - MongoDB
  - mongoimport
  - JSON
  - Database
description: "mongoimportコマンドを使ってMongoDBにJSON形式のデータをインポートする方法を解説します。便利なオプションも併せて紹介し、実務で役立つポイントをまとめました。"
---

## Table of Contents

## Introduction

MongoDBにJSONデータをインポートする場合、mongoimportコマンドが非常に便利です。mongoimportを使用すると、ターミナルやコマンドプロンプトから直接MongoDBのデータベースにJSONファイルを取り込むことができます。本記事では、基本的なインポート手順と、知っておくと便利なmongoimportのオプションについて解説します。

## mongoimportの基本的な使い方

mongoimportは、JSONやCSVなどのデータファイルをMongoDBのデータベースに直接インポートするためのツールで、MongoDBのインストール時に一緒にインストールされます。インポートしたいデータがJSONファイルの場合、以下のようにmongoimportを使用します。

## 基本コマンド

```
mongoimport --db <データベース名> --collection <コレクション名> --file <ファイルパス> --jsonArray
```

コマンドの実行手順

    1.	JSONファイルの準備

MongoDBにインポートしたいデータをJSON形式で用意します。ファイルは配列形式で用意しておくと便利です。例として、sample.jsonというファイルを用意します。

```
[
    { "name": "Alice", "age": 25 },
    { "name": "Bob", "age": 30 },
    { "name": "Charlie", "age": 35 }
]
```

    2.	mongoimportコマンドの実行

ターミナルまたはコマンドプロンプトで、以下のコマンドを実行して、sample.jsonをmyDatabaseというデータベースのmyCollectionというコレクションにインポートします。

mongoimport --db myDatabase --collection myCollection --file sample.json --jsonArray

ここで各パラメータの意味は以下の通りです：
• --db <データベース名>：インポート先のデータベース名
• --collection <コレクション名>：インポート先のコレクション名
• --file <ファイルパス>：インポートするJSONファイルのパス
• --jsonArray：JSONファイルが配列形式の場合に指定

## 便利なオプションと補足情報

### オプションについて

    •	--jsonArrayオプションの省略

--jsonArrayオプションを省略すると、ファイル内のJSONが1行ずつ独立したドキュメントとして扱われます。もしJSONデータが配列形式でない場合や、1行ごとにJSONオブジェクトが記載されている場合は、このオプションを省略できます。
• --upsertオプション
既存データを更新したり、新しいデータを追加するには、--upsertオプションを使用します。このオプションを使うと、インポート時に既存のドキュメントをキーで確認し、既存の場合は更新、存在しない場合は新規追加されます。

```
mongoimport --db myDatabase --collection myCollection --file sample.json --jsonArray --upsert
```

    •	--dropオプション

インポート前にコレクション内のデータを削除する場合、--dropオプションを指定します。データを上書きする際に便利です。

mongoimport --db myDatabase --collection myCollection --file sample.json --jsonArray --drop

    •	--typeオプション

mongoimportはデフォルトでJSON形式をインポートしますが、CSVやTSVファイルのインポートも可能です。ファイル形式に応じて--typeオプションを指定します。

```
mongoimport --db myDatabase --collection myCollection --type csv --file sample.csv --headerline
```

CSVの場合、--headerlineオプションを使用すると、最初の行をフィールド名として扱います。

よくあるエラーと対策

    •	JSONファイル形式の不備

インポートするJSONファイルが不正な形式の場合、エラーが発生します。ファイルの末尾や各ドキュメントのカンマなどに注意して、事前にファイルの形式を確認してください。
• パーミッションエラー
mongoimportを実行する際、MongoDBに書き込み権限が必要です。アクセス権限が不足している場合、適切な権限を持つユーザーで実行するか、必要に応じてユーザーを追加してください。

## Conclusion

mongoimportコマンドを使用することで、MongoDBへのJSONファイルのインポートが簡単に行えます。また、--upsertや--dropオプションを活用することで、データの更新や削除を効率的に管理できます。これらのオプションを知っておくことで、柔軟かつ効率的なデータ操作が可能になります。
