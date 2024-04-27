---
author: Taro Gray
pubDatetime: 2024-04-27T12:09:00.00Z
title: Java Design Pattern Strategy Method について
postSlug: java-design-strategy-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Strategy Method
description: Strategy パターンは、アルゴリズムのファミリーを定義し、それぞれをカプセル化して交換可能にするデザインパターンです。このパターンを使用することで、アルゴリズムを使用するクライアントとは独立してアルゴリズムを変更することが可能です。Strategy パターンは、特定のタスクを実行するための異なる方法が必要な場合に特に有効です。
---

## Table of contents

## パターンの概要

Strategy パターンは主に以下の3つのコンポーネントで構成されます：

1. **Context（コンテキスト）**: Strategy オブジェクトを使用するクラス。クライアントが使用するインターフェースを提供し、Strategy オブジェクトにアルゴリズムの実行を委譲します。
2. **Strategy（ストラテジー）**: すべてのアルゴリズムファミリーで共通のインターフェースまたは抽象クラス。
3. **ConcreteStrategy（具体的なストラテジー）**: Strategy クラスの具体的な実装で、具体的なアルゴリズムをカプセル化します。

## Strategy パターンの利点

- **柔軟性の向上**: クライアントは実行時にアルゴリズムを自由に交換できるため、より柔軟なコードが可能になります。
- **再利用性と分離**: 各アルゴリズムが独立してカプセル化されているため、異なるコンテキストで再利用することが容易です。
- **拡張性**: 新しいアルゴリズムを追加するときは、新しい ConcreteStrategy クラスを作成するだけで、既存のコードに影響を与えることなく実装できます。

## 実装例

```java
// Strategy
interface SortingStrategy {
    void sort(int[] data);
}

// ConcreteStrategy
class QuickSort implements SortingStrategy {
    public void sort(int[] data) {
        // クイックソートの実装
        System.out.println("QuickSort");
    }
}

class MergeSort implements SortingStrategy {
    public void sort(int[] data) {
        // マージソートの実装
        System.out.println("MergeSort");
    }
}

// Context
class SortedList {
    private SortingStrategy strategy;
    private int[] data;

    public SortedList(int[] data) {
        this.data = data;
    }

    public void setSortingStrategy(SortingStrategy strategy) {
        this.strategy = strategy;
    }

    public void sortData() {
        strategy.sort(data);
    }
}

// Client
public class StrategyDemo {
    public static void main(String[] args) {
        int[] data = {34, 7, 23, 32, 5};
        SortedList list = new SortedList(data);

        list.setSortingStrategy(new QuickSort());
        list.sortData();

        list.setSortingStrategy(new MergeSort());
        list.sortData();
    }
}
```

## 関連記事

Strategy パターンに関してさらに詳しく学びたい場合は、以下の記事が役立ちます。

1. **Refactoring Guru** - [Strategy Pattern](https://refactoring.guru/design-patterns/strategy)

   - この記事では、Strategy パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Strategy Design Pattern](https://sourcemaking.com/design_patterns/strategy)
   - Strategy パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介
