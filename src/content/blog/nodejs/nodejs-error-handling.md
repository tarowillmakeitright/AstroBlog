---
author: Taro Gray
pubDatetime: 2023-12-03T05:03:00.00Z
title: Node.jsのエラーハンドリング：面白く学ぶエラー処理
postSlug: nodejs-error-handling
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - NodeJS
  - error-handling
description: Node.jsでのエラーハンドリングは、ロバストなアプリケーション開発に不可欠です。この記事では、エラーハンドリングの基本から、より高度なテクニックまでを面白い例とともに解説します。
---

## Table of contents

## Node.jsのエラーハンドリング：面白く学ぶエラー処理

Node.jsでのエラーハンドリングは、ロバストなアプリケーション開発に不可欠です。この記事では、エラーハンドリングの基本から、より高度なテクニックまでを面白い例とともに解説します。

## 1. 'JSON.parse()'のエラーハンドリング

`JSON.parse()`は、不正なJSONを解析しようとした際にエラーを投げます。これを適切にハンドリングしましょう。

```javascript
function safeParse(jsonString) {
  try {
    return JSON.parse(jsonString);
  } catch (e) {
    console.error("Invalid JSON:", e.message);
    return null;
  }
}

const data = safeParse('{"name": "Alice"}'); // 正しいJSON
const badData = safeParse('{"name", "Alice"}'); // 不正なJSON
```

## 2. 未処理の例外

Node.jsでは、未処理の例外が発生するとプロセスがクラッシュします。これを防ぐために、グローバルなエラーハンドラを設定できます。

```javascript
process.on("uncaughtException", error => {
  console.error("Uncaught Exception:", error);
  // 必要なクリーンアップ処理をここに記述
});

// 故意にエラーを発生させる
throw new Error("Oops!");
```

## 3. parseJsonAsync()

非同期処理中のエラーを適切にハンドリングする方法を見てみましょう。

```javascript
function parseJsonAsync(jsonString) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      try {
        resolve(JSON.parse(jsonString));
      } catch (e) {
        reject(e);
      }
    }, 1000);
  });
}

parseJsonAsync('{"name": "Alice"}')
  .then(data => console.log(data))
  .catch(err => console.error("Error parsing JSON:", err));
```

## 4. 面白い例：ハッカーのエラーハンドリング

ハッカーもエラーハンドリングには注意が必要です。彼らはしばしば、予期せぬ入力や状況に直面します。

```javascript
function hackTheMainframe(input) {
  try {
    // 複雑なハッキングロジック...
    if (input === "unexpected") {
      throw new Error("Unexpected input!");
    }
    console.log("Hacking successful!");
  } catch (e) {
    console.error("Hacking failed:", e.message);
  }
}

hackTheMainframe("expected");
hackTheMainframe("unexpected");
```

この架空の例では、ハッカーは予期せぬ入力に対してエラーハンドリングを行っています。

## まとめ

エラーハンドリングは、信頼性の高いNode.jsアプリケーション開発において不可欠です。面白い例を通じて、エラーハンドリングの重要性を理解し、楽しんで学んでいただければと思います。ハッピーハッキング！
