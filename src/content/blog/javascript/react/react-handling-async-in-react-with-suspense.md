---
author: Taro Gray
pubDatetime: 2024-06-30T15:56:00.00Z
title: ReactのSuspenseと非同期処理の扱い方
postSlug: react-handling-async-in-react-with-suspense
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - JavaScript
  - React
  - Async
  - Suspense
description: ReactのSuspenseを使用して、非同期データをエレガントに扱う方法を解説します。この機能を使うと、ローディング状態の管理が簡単になり、ユーザー体験が向上します。
---

## 目次

## ReactのSuspenseとは？

ReactのSuspenseは、コンポーネントがデータの読み込みを待っている間、フォールバックコンテンツを表示するための機能です。これにより、非同期データの取得中に「ローディング...」などのプレースホルダーを表示することが可能になります。

## 非同期処理の基本

非同期処理はJavaScriptで広く利用されており、Promiseを使うことが一般的です。Promiseは、非同期操作が成功(fulfilled)、失敗(rejected)、またはまだ結果が出ていない(pending)のいずれかの状態を持ちます。

## Suspenseを使った非同期データのハンドリング

以下は、Suspenseと非同期処理を組み合わせたReactコンポーネントの例です。

```jsx
import React, { Suspense } from "react";
import ThrowPromise from "./ThrowPromise";

function SuspenseResult() {
  return (
    <Suspense fallback={<p>Now Loading...</p>}>
      <ThrowPromise />
    </Suspense>
  );
}

export default SuspenseResult;
```

この例では、`ThrowPromise` コンポーネントがデータの取得を試み、データがロードされるまで `<Suspense>` コンポーネントがフォールバックコンテンツを表示します。

## Promiseの活用例

```jsx
function ThrowPromise() {
  let flag = false;

  if (!flag) {
    throw new Promise((resolve, reject) => {
      setTimeout(() => {
        resolve("Success!");
        flag = true;
      }, 3000);
    });
  }

  return <p>データが読み込まれました。</p>;
}
```

このコードでは、`ThrowPromise` が初めてレンダーされた際に、条件式が `false` であるため、Promiseが投げられ、Suspenseによってキャッチされます。3秒後にPromiseが解決され、コンポーネントが再レンダーされます。

## まとめ

ReactのSuspenseを使うことで、非同期データの取得とその表示をスムーズに管理することができます。この機能により、データがロードされる間のユーザー体験を大きく向上させることが可能です。開発者は、非同期処理をより効果的に扱えるようになります。

このブログでは、ReactのSuspenseとPromiseの基本的な使い方を紹介しました。これを基に、より複雑な非同期処理のシナリオを開発する際の参考にしてください。
