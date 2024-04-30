---
author: Taro Gray
pubDatetime: 2024-04-27T13:37:00.00Z
title: Java Design Pattern State Method について
postSlug: java-design-state-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - State Method
description: State パターンは、オブジェクトの内部状態が変化するとその行動が変わるような状況で使用されるデザインパターンです。このパターンは、オブジェクトの状態を表すクラス群を通じて状態依存の振る舞いをカプセル化し、実行時にオブジェクトのクラスを変更することなくその振る舞いを変更できるようにします。
---

## Table of contents

## State パターンの探究

State パターンは、オブジェクトの内部状態が変化するとその行動が変わるような状況で使用されるデザインパターンです。このパターンは、オブジェクトの状態を表すクラス群を通じて状態依存の振る舞いをカプセル化し、実行時にオブジェクトのクラスを変更することなくその振る舞いを変更できるようにします。

## パターンの構成要素

1. **Context (コンテキスト)**: 現在の状態を持ち、状態に依存した振る舞いを実行するために状態オブジェクトを使用するクラスです。
2. **State (状態)**: ある特定の状態での振る舞いを定義するインターフェースまたは抽象クラス。
3. **Concrete States (具体的な状態)**: State インターフェースまたは抽象クラスを実装または継承し、特定の状態における具体的な振る舞いを定義するクラス。

## State パターンの利点

- **柔軟性の向上**: 新しい状態クラスを追加することで簡単に新しい状態と振る舞いを導入できます。
- **カプセル化の強化**: 状態ごとの振る舞いを状態クラス内にカプセル化することで、それぞれの状態のロジックを独立させ、お互いから分離します。
- **クラス爆発の防止**: 状態遷移のロジックを独立したクラスに分割することで、コンテキストクラスをシンプルに保ち、クラス爆発を避けることができます。

## 実装例

```java
// State
interface State {
    void handle(Context context);
}

// Concrete States
class StartState implements State {
    public void handle(Context context) {
        System.out.println("Player is in start state");
        context.setState(this);
    }

    public String toString() {
        return "Start State";
    }
}

class StopState implements State {
    public void handle(Context context) {
        System.out.println("Player is in stop state");
        context.setState(this);
    }

    public String toString() {
        return "Stop State";
    }
}

// Context
class Context {
    private State state;

    public Context() {
        state = null;
    }

    public void setState(State state) {
        this.state = state;
    }

    public State getState() {
        return state;
    }
}

// Client
public class StatePatternDemo {
    public static void main(String[] args) {
        Context context = new Context();

        StartState startState = new StartState();
        startState.handle(context);

        System.out.println(context.getState().toString());

        StopState stopState = new StopState();
        stopState.handle(context);

        System.out.println(context.getState().toString());
    }
}
```

## 関連記事

State パターンについてさらに学びたい場合は、以下の記事が役立ちます：

1. **Refactoring Guru** - [State Pattern](https://refactoring.guru/design-patterns/state)

   - この記事では、State パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [State Design Pattern](https://sourcemaking.com/design_patterns/state)
   - State パターンの背景、動機、構造について
