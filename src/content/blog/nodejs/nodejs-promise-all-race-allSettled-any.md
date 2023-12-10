---
author: Taro Gray
pubDatetime: 2023-12-10T23:41:00.00Z
title: Node.jsのPromiseスタティックメソッド：非同期処理の並行実行マスターへの道
postSlug: nodejs-promise-all-race-allSettled-any
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - NodeJS
  - Promise
description: Node.jsにおける非同期処理は、Promiseのスタティックメソッドを使用することで、より効率的かつ柔軟に実行できます。この記事では、`Promise.all`、`Promise.race`、`Promise.allSettled`、`Promise.any`の使い方を面白い例と共に探ります。
---

## Table of contents

## Node.jsのPromiseスタティックメソッド：非同期処理の並行実行マスターへの道

Node.jsにおける非同期処理は、Promiseのスタティックメソッドを使用することで、より効率的かつ柔軟に実行できます。この記事では、`Promise.all`、`Promise.race`、`Promise.allSettled`、`Promise.any`の使い方を面白い例と共に探ります。

## 1. `Promise.all`

`Promise.all`は、複数のPromiseが全て成功するのを待ちます。

```javascript
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise(resolve => setTimeout(resolve, 100, "foo"));

Promise.all([promise1, promise2, promise3]).then(values => {
  console.log(values); // [3, 42, "foo"]
});
```

## 2. `Promise.race`

`Promise.race`は、最初に解決または拒否されるPromiseの結果を返します。

```javascript
const promise1 = new Promise((resolve, reject) =>
  setTimeout(resolve, 500, "one")
);
const promise2 = new Promise((resolve, reject) =>
  setTimeout(reject, 100, "two")
);

Promise.race([promise1, promise2])
  .then(value => {
    console.log(value);
  })
  .catch(reason => {
    console.log(reason); // "two"
  });
```

## 3. `Promise.allSettled`

`Promise.allSettled`は、全てのPromiseが解決または拒否されるのを待ちます。

```javascript
const promise1 = Promise.resolve(3);
const promise2 = new Promise((resolve, reject) =>
  setTimeout(reject, 100, "two")
);

Promise.allSettled([promise1, promise2]).then(results => {
  results.forEach(result => console.log(result.status));
});
```

## 4. `Promise.any`

`Promise.any`は、最初に成功するPromiseの結果を返します。

```javascript
const promise1 = new Promise((resolve, reject) =>
  setTimeout(reject, 500, "one")
);
const promise2 = new Promise((resolve, reject) =>
  setTimeout(resolve, 100, "two")
);

Promise.any([promise1, promise2]).then(value => {
  console.log(value); // "two"
});
```

## 5. 面白い例：ハッカーの非同期作戦

面白い例として、ハッカーが複数のサイバー攻撃を同時に実行し、最初に成功したものを利用するシナリオを考えてみましょう。

```javascript
const hackServer = new Promise(resolve =>
  setTimeout(resolve, 300, "Server hacked")
);
const crackPassword = new Promise(resolve =>
  setTimeout(resolve, 600, "Password cracked")
);
const breachFirewall = new Promise((resolve, reject) =>
  setTimeout(reject, 200, "Firewall breach failed")
);

Promise.any([hackServer, crackPassword, breachFirewall])
  .then(firstSuccess => {
    console.log(firstSuccess);
  })
  .catch(() => {
    console.log("All hacking attempts failed");
  });
```

この架空の例では、ハッカーが複数の攻撃を同時に実行し、最初に成功した攻撃を利用しています。

Promiseのスタティックメソッドは、複雑な非同期処理を管理する上で非常に有効です。面白い例を通じて、これらのメソッドの使い方を理解し、楽しんで学んでいただければと思います。ハッピーハッキング！
