---
author: Taro Gray
pubDatetime: 2024-07-07T17:51:00.00Z
title: カスタムフックの作成 useCounterを例に
postSlug: react-creating-custom-hooks-usecounter-example
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - JavaScript
  - React
  - Custom Hooks
description: Reactでカスタムフックを自作する方法を、useCounterフックを例に詳しく解説します。このフックはカウンター機能を提供し、任意の初期値とステップ値でインクリメントやデクリメントが可能です。
---

## 目次

## カスタムフックとは？

カスタムフックは、Reactの再利用可能なロジックをカプセル化する手法です。これにより、コンポーネント間で状態や副作用の管理ロジックを共有することができます。今回は、シンプルなカウンター機能を実装するカスタムフック`useCounter`を作成します。

## useCounterフックの作成

useCounterフックは、カウンターの現在値とその操作を提供します。これにより、任意のコンポーネントでカウンター機能を簡単に実装できます。

```javascript
import { useReducer } from "react";

function useCounter(init, step) {
  const initialState = { count: init };
  const reducer = (state, action) => {
    switch (action.type) {
      case "update":
        return { count: state.count + action.step };
      case "reset":
        return { count: action.init };
      default:
        return state;
    }
  };

  const [state, dispatch] = useReducer(reducer, initialState);

  const handleUp = () => dispatch({ type: "update", step });
  const handleDown = () => dispatch({ type: "update", step: -step });
  const handleReset = () => dispatch({ type: "reset", init });

  return [state, handleUp, handleDown, handleReset];
}
```

## useCounterの使用方法

カスタムフック`useCounter`は以下のようにして使用できます：

```javascript
function CounterComponent() {
  const [state, handleUp, handleDown, handleReset] = useCounter(0, 1);

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={handleUp}>Increase</button>
      <button onClick={handleDown}>Decrease</button>
      <button onClick={handleReset}>Reset</button>
    </div>
  );
}
```

このコンポーネントでは、カウンターの値を増減させるボタンと、値を初期値にリセットするボタンが提供されています。

## まとめ

`useCounter`のようなカスタムフックを作成することで、アプリケーション全体でロジックを再利用し、コードの整理とメンテナンスが容易になります。また、カスタムフックは特定のUIに依存しないため、多様なシナリオで使用することができます。この方法を通じて、より効率的かつ効果的なReactアプリケーションを構築しましょう。react-
