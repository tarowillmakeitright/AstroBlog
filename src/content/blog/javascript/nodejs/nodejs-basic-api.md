---
author: Taro Gray
pubDatetime: 2023-12-17T23:50:00.00Z
title: Node.jsのExpressでFetchを活用する：GETとPOSTリクエストの扱い
postSlug: nodejs-get-post
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - NodeJS
  - express
  - get
  - post
description:
---

## Table of contents

了解しました！Node.jsのExpressフレームワークで`fetch`を使ったGETおよびPOSTリクエストの取り扱いに関するブログ記事をMarkdown形式で作成します。面白いコード例と、ハッカーに関連する情報も組み込みます。それでは、以下のブログ記事をご覧ください。

---

## Node.jsのExpressでFetchを活用する：GETとPOSTリクエストの扱い

Node.jsのExpressフレームワークは、Webサーバーの構築に欠かせないツールです。この記事では、フロントエンドから`fetch`を使ってExpressサーバーにGETおよびPOSTリクエストを送信する方法を面白い例と共に解説します。

## 1. ExpressでのGETリクエストの処理

ExpressでGETリクエストを処理する方法は非常にシンプルです。

```javascript
const express = require("express");
const app = express();

app.get("/api/data", (req, res) => {
  res.json({ message: "Hello from server!" });
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

## 2. ExpressでのPOSTリクエストの処理

ExpressでPOSTリクエストを処理するためには、まず`express.json()`ミドルウェアを使用して、JSONデータの解析を行います。

```javascript
app.use(express.json());

app.post("/api/data", (req, res) => {
  console.log(req.body); // リクエストのボディを表示
  res.json({ message: "Data received!" });
});
```

## 3. フロントエンドからのFetchリクエスト

フロントエンドからExpressサーバーにリクエストを送信するためには、`fetch`APIを使用します。

### GETリクエスト

```javascript
fetch("/api/data")
  .then(response => response.json())
  .then(data => console.log(data));
```

### POSTリクエスト

```javascript
fetch("/api/data", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ name: "Alice" }),
})
  .then(response => response.json())
  .then(data => console.log(data));
```

## 4. 面白い例：宇宙旅行エージェンシーのAPI

宇宙旅行に関する情報を扱うAPIを作成してみましょう。

```javascript
app.get("/api/spaceships", (req, res) => {
  res.json({ spaceship: "Galaxy Cruiser" });
});

app.post("/api/book-trip", (req, res) => {
  console.log(`Booking trip to ${req.body.destination}`);
  res.json({ message: `Trip booked to ${req.body.destination}` });
});
```

## 5. ハッカーとFetchの使用

ハッカーは、Fetch APIを使って、サーバーから機密情報を抜き取る攻撃を仕掛けることがあります。

```javascript
fetch("/api/secret-data", {
  method: "GET",
  headers: { Authorization: "Bearer fake-token" },
})
  .then(response => response.json())
  .then(data => console.log("Stolen data:", data));
```

ExpressとFetch APIを使うことで、フロントエンドとバックエンドの間のデータのやり取りがスムーズに行えます。この記事で紹介した方法を通じて、効率的なWebアプリケーション開発のスキルを身につけましょう。ハッピーハッキング！
