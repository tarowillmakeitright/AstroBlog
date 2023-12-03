---
author: Taro Gray
pubDatetime: 2023-12-03T05:52:00.007Z
title: Node.jsで楽しむPromise：生成から状態遷移まで
postSlug: javascript-promise
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Javascript
  - promise
description: Node.jsの非同期処理におけるPromiseは、コードの読みやすさと管理のしやすさを大きく改善します。この記事では、Promiseの生成と状態遷移について面白い例を交えて解説します。
---

## Table of contents

## Node.jsで楽しむPromise：生成から状態遷移まで

Node.jsの非同期処理におけるPromiseは、コードの読みやすさと管理のしやすさを大きく改善します。この記事では、Promiseの生成と状態遷移について面白い例を交えて解説します。

## 1. Promiseの基本

Promiseは、非同期処理の最終的な成功（resolve）または失敗（reject）を表すオブジェクトです。

```javascript
const myPromise = new Promise((resolve, reject) => {
  const condition = true;
  if (condition) {
    resolve("Promise is resolved!");
  } else {
    reject("Promise is rejected!");
  }
});

myPromise
  .then(result => console.log(result)) // Promise is resolved!
  .catch(error => console.log(error));
```

## 2. Promiseの状態遷移

Promiseには3つの状態があります：`pending`、`fulfilled`、`rejected`。

- **pending**: 初期状態。成功も失敗もしていない。
- **fulfilled**: 処理が成功し、結果が利用可能。
- **rejected**: 処理が失敗し、エラーが発生。

## 3. 面白い例：時間旅行のPromise

面白い例として、時間旅行を試みるPromiseを考えてみましょう。

```javascript
function timeTravel(destination) {
  return new Promise((resolve, reject) => {
    console.log(`Attempting to travel to ${destination}`);
    setTimeout(() => {
      if (destination === "future") {
        resolve("Welcome to the future!");
      } else if (destination === "past") {
        reject("Failed to travel to the past.");
      }
    }, 3000);
  });
}

timeTravel("future")
  .then(result => console.log(result))
  .catch(error => console.log(error));
```

この架空の例では、`timeTravel`関数は未来への旅は成功するが、過去への旅は失敗するというPromiseを返します。

## 4. ハッカーとPromise

ハッカーもPromiseを使って、非同期のネットワーク攻撃やデータ収集を行うことがあります。

```javascript
function hackNetwork() {
  return new Promise((resolve, reject) => {
    // ハッキングの試み...
    setTimeout(() => {
      const success = Math.random() > 0.5;
      if (success) {
        resolve("Network hacked!");
      } else {
        reject("Hacking attempt failed.");
      }
    }, 2000);
  });
}

hackNetwork()
  .then(result => console.log(result))
  .catch(error => console.log(error));
```

## まとめ

この架空の例では、ハッカーがネットワークをハックしようとする非同期プロセスをPromiseで表現しています。
Promiseは、Node.jsでの非同期処理をより扱いやすくします。面白い例を通じて、Promiseの概念を理解し、楽しんで学んでいただければと思います。ハッピーハッキング！
