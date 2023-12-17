---
author: Taro Gray
pubDatetime: 2023-12-18T00:08:00.00Z
title: ReactのuseEffectフック：ユニークな例で学ぶ
postSlug: react-useEffect
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - React
  - useEffect
description: Reactの `useEffect` は、関数コンポーネントの副作用を扱うためのフックです。この記事では、`useEffect` の基本と、ユニークな例を紹介します。
---

## Table of contents

## ReactのuseEffectフック：ユニークな例で学ぶ

Reactの `useEffect` は、関数コンポーネントの副作用を扱うためのフックです。この記事では、`useEffect` の基本と、ユニークな例を紹介します。

## 基本的な使い方

`useEffect` は、コンポーネントがレンダリングされた後に何かを実行したい場合に使います。

```javascript
import React, { useState, useEffect } from "react";

function ExampleComponent() {
  const [count, setCount] = useState(0);

  // useEffectを使って、countが更新されるたびに何かを行います
  useEffect(() => {
    document.title = `あなたがクリックした回数： ${count} 回`;
  });

  return (
    <div>
      <p>カウント: {count}</p>
      <button onClick={() => setCount(count + 1)}>カウントアップ</button>
    </div>
  );
}
```

この例では、カウントが更新されるたびにブラウザのタイトルが更新されます。

## 面白い例：ハッカー風タイマー

ここで、`useEffect` を使った面白い例を紹介しましょう。ハッカー風タイマーを作ってみます。

```javascript
import React, { useState, useEffect } from "react";

function HackerTimer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(prevSeconds => prevSeconds + 1);
    }, 1000);

    // クリーンアップ関数でインターバルをクリア
    return () => clearInterval(interval);
  }, []);

  return (
    <div>
      <p>ハッキング時間: {seconds} 秒</p>
    </div>
  );
}
```

このコンポーネントでは、ハッキングしているかのように秒数をカウントアップして表示します。`useEffect` のクリーンアップ関数でタイマーを正しく管理しています。
`useEffect` を使うと、副作用のある処理を効果的に扱うことができます。面白いアイデアで、ユーザーを楽しませてみてください！
