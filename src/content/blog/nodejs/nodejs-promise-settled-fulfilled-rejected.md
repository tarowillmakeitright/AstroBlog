---
author:
pubDatetime: 2023-12-10T23:41:00.00Z
title: Node.jsのPromiseの状態：`Settled`、`Fulfilled`、`Rejected`を理解しよう
postSlug: nodejs-promise-settled-fulfilled-rejected
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - NodeJS
  - Promise
description: Promiseは非同期プログラミングの核となる概念で、`settled`、`fulfilled`、`rejected`という3つの状態があります。この記事では、これらの状態とその違いを面白い例を交えて解説します。
---

## Table of contents

## Node.jsのPromiseの状態：`Settled`、`Fulfilled`、`Rejected`を理解しよう

Promiseは非同期プログラミングの核となる概念で、`settled`、`fulfilled`、`rejected`という3つの状態があります。この記事では、これらの状態とその違いを面白い例を交えて解説します。

## 1. `Fulfilled`

Promiseが成功的に解決された状態を`fulfilled`といいます。

```javascript
const promiseFulfilled = Promise.resolve("Success!");

promiseFulfilled.then(result => {
  console.log(result); // "Success!"
});
```

## 2. `Rejected`

Promiseがエラーにより拒否された状態を`rejected`といいます。

```javascript
const promiseRejected = Promise.reject("Error occurred!");

promiseRejected.catch(error => {
  console.error(error); // "Error occurred!"
});
```

## 3. `Settled`

Promiseが`fulfilled`または`rejected`のいずれかの状態になったことを意味する`settled`。

```javascript
const promise1 = Promise.resolve(3);
const promise2 = Promise.reject(new Error("An error"));

Promise.allSettled([promise1, promise2]).then(results => {
  results.forEach(result => console.log(result.status));
  // "fulfilled", "rejected"
});
```

## 4. 面白い例：ハッカーのプロミス

面白い例として、ハッカーが複数の攻撃を実行し、それぞれの結果をプロミスで管理するシナリオを考えてみましょう。

```javascript
const hackServer = new Promise(resolve =>
  setTimeout(resolve, 300, "Server hacked")
);
const crackPassword = new Promise((resolve, reject) =>
  setTimeout(reject, 600, "Failed to crack password")
);

Promise.allSettled([hackServer, crackPassword]).then(results => {
  results.forEach(result => {
    if (result.status === "fulfilled") {
      console.log(`Success: ${result.value}`);
    } else {
      console.log(`Failure: ${result.reason}`);
    }
  });
});
```

この架空の例では、ハッカーがサーバーをハックし、パスワードを解読しようとしますが、一つのタスクは成功し、もう一つは失敗します。
Promiseの`settled`、`fulfilled`、`rejected`の状態は、非同期処理の結果を正確に管理するために不可欠です。面白い例を通じて、これらの状態とその違いを理解し、楽しんで学んでいただければと思います。ハッピーハッキング！
