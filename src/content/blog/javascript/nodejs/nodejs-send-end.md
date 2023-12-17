---
author: Taro Gray
pubDatetime: 2023-12-17T23:44:00.00Z
title: Expressの`res.send`と`res.end`：応答を上手に送る
postSlug: nodejs-send-end
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - NodeJS
  - express
  - send
  - end
description: Node.jsのExpressフレームワークでは、`res.send`と`res.end`メソッドを使ってクライアントに応答を送ることができます。この記事では、これらのメソッドの違いと使い方を面白い例を交えて解説します。
---

## Table of contents

## Expressの`res.send`と`res.end`：応答を上手に送る

Node.jsのExpressフレームワークでは、`res.send`と`res.end`メソッドを使ってクライアントに応答を送ることができます。この記事では、これらのメソッドの違いと使い方を面白い例を交えて解説します。

## 1. `res.send`の基本

`res.send`は、様々なタイプのレスポンスを送るために使われます。テキスト、HTML、JSONなど、自動的に適切なContent-Typeを設定してくれます。

```javascript
const express = require("express");
const app = express();

app.get("/", (req, res) => {
  res.send("Hello World!");
});

app.listen(3000, () => {
  console.log("Server running on port 3000");
});
```

## 2. `res.end`の使い方

`res.end`は、応答を終了させるために使用されますが、`res.send`と異なり、任意のデータを送ることはありません。

```javascript
app.get("/end", (req, res) => {
  res.end();
});
```

## 3. `res.send`と`res.end`の違い

`res.send`はデータと共に応答を終了させますが、`res.end`は応答を終了させるだけで、データの送信は行いません。

## 4. 面白い例：宇宙観測所のAPI

宇宙観測所のAPIを提供するサーバを作ってみましょう。

```javascript
app.get("/space", (req, res) => {
  const data = { stars: 100, galaxies: 20 };
  res.send(data);
});

app.get("/space/end", (req, res) => {
  console.log("Connection ended without data");
  res.end();
});
```

## 5. ハッカーと`res.end`

ハッカーがサーバーへの攻撃を試みた場合、`res.end`を使用して、情報を一切送らずに接続を切断することができます。

```javascript
app.get("/secret", (req, res) => {
  if (!isAuthorized(req)) {
    res.end();
  } else {
    res.send("Secret data");
  }
});
```

Expressの`res.send`と`res.end`は、Webサーバーの応答を管理する上で非常に重要なツールです。この記事で紹介した面白い例を通じて、それぞれのメソッドの違いと使い方を楽しく学んでいただければと思います。ハッピーハッキング！
