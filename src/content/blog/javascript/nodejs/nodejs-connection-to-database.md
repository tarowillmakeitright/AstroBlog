---
author: Taro Gray
pubDatetime: 2023-12-17T23:39:00.00Z
title: Node.jsでデータベースに接続：セキュリティと利便性を両立
postSlug: nodejs-connection-to-database
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - NodeJS
  - database
description: Node.jsを使用したWebアプリケーションでは、データベースとの連携が不可欠です。この記事では、環境変数を利用して安全にデータベースに接続する方法を面白い例と共に探ります。
---

## Table of contents

## Node.jsでデータベースに接続：セキュリティと利便性を両立

Node.jsを使用したWebアプリケーションでは、データベースとの連携が不可欠です。この記事では、環境変数を利用して安全にデータベースに接続する方法を面白い例と共に探ります。

## 1. 環境変数と`.env`ファイル

データベース接続情報などの機密情報は、環境変数に保存することでセキュリティを高めることができます。`.env`ファイルを使用すると、これらの環境変数を簡単に管理できます。

まずは`dotenv`パッケージをプロジェクトに追加します。

```bash
npm install dotenv
```

`.env`ファイルをプロジェクトのルートに作成し、接続情報を記述します。

```
DB_HOST=localhost
DB_USER=root
DB_PASS=s1mpl3
```

アプリケーションで`dotenv`を読み込み、環境変数を使用します。

```javascript
require("dotenv").config();

const dbConfig = {
  host: process.env.DB_HOST,
  user: process.env.DB_USER,
  password: process.env.DB_PASS,
};

console.log("Database Config:", dbConfig);
```

## 2. データベースへの接続

ここではMySQLを例に、データベースへの接続方法を示します。

```javascript
const mysql = require("mysql");

const connection = mysql.createConnection(dbConfig);

connection.connect(error => {
  if (error) throw error;
  console.log("Successfully connected to the database.");
});
```

## 3. 面白い例：宇宙データベース

宇宙に関する情報を扱うデータベースに接続する例を考えてみましょう。

```javascript
connection.query("SELECT * FROM planets", (error, results, fields) => {
  if (error) throw error;
  results.forEach(planet => {
    console.log(planet.name);
  });
});
```

この例では、惑星に関する情報をデータベースから取得しています。

## 4. ハッカーとデータベースのセキュリティ

ハッカーは、セキュリティが不十分なデータベースにアクセスしようとすることがあります。`.env`ファイルを使用することで、重要な情報をコードから分離し、セキュリティを向上させることができます。

```javascript
// 悪意のあるハッカーが狙う可能性のある情報
const sensitiveQuery = "SELECT * FROM users WHERE user='admin'";
connection.query(sensitiveQuery, (error, results) => {
  // ...
});
```

この架空の例では、ハッカーが管理者の情報を抽出しようとしています。
Node.jsでのデータベース連携は、アプリケーションの機能を強化し、ユーザー体験を豊かにします。この記事で紹介した方法を通じて、安全かつ効果的なデータベース接続を実現しましょう。ハッピ
