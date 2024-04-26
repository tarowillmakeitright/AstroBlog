---
author: Taro Gray
pubDatetime: 2024-04-26T16:43:00.00Z
title: [Java Design Pattern] Prototype パターンの解説
postSlug: java-prototype-pattern-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Design Pattern
  - Prototype Method Pattern
description: Prototype パターンは、デザインパターンの一つで、既存のオブジェクトをプロトタイプとして使用し、オブジェクトのクローニングを通じて新しいオブジェクトを生成する方法です。このパターンは、オブジェクトの作成が高コストである場合や、クライアントがクラスの実装ではなくインターフェースに依存するべき場合に特に有効です。
---

## Table of contents

## パターンの目的

Prototype パターンの主な目的は、新しいインスタンスを作成するために直接コンストラクタを呼び出す代わりに、既存のオブジェクトを複製することによってオブジェクトの生成コストを削減することです。これにより、動的なシステム拡張が可能となり、複雑なオブジェクトのセットアッププロセスを簡略化できます。

## パターンの構成要素

1. **Prototype** - クローンを生成するためのインターフェースを提供するクラス。
2. **Concrete Prototype** - `Prototype` インターフェースを実装し、自己の複製を作成する具体的なクラス。
3. **Client** - `Prototype` インターフェースを使用して新しいオブジェクトを複製するクラス。

## コード例

Java での Prototype パターンの一般的な実装は以下の通りです。

```java
// Prototype
public interface Prototype {
    Prototype clone();
}

// Concrete Prototype
public class ConcretePrototype implements Prototype {
    private int x;

    public ConcretePrototype(int x) {
        this.x = x;
    }

    @Override
    public Prototype clone() {
        return new ConcretePrototype(this.x);
    }
}

// Client
public class Client {
    public static void main(String[] args) {
        ConcretePrototype original = new ConcretePrototype(100);
        ConcretePrototype clone = (ConcretePrototype) original.clone();
        System.out.println("Original: " + original.getX());
        System.out.println("Clone: " + clone.getX());
    }
}
```

## 関連記事

Prototype パターンのさらなる理解を深めるために、以下の記事を参考にすることをお勧めします。

1. **Refactoring Guru** - [Prototype Pattern](https://refactoring.guru/design-patterns/prototype)

   - Prototype パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Prototype Design Pattern](https://sourcemaking.com/design_patterns/singleton)
