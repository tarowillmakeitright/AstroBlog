---
author: Taro Gray
pubDatetime: 2024-04-26T11:46:00.00Z
title: Java Design Pattern Abstract Factory Method について
postSlug: java-design-abstract-factory-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Abstract Factory Method
description: Abstract Factory パターンは、関連性のある一連のオブジェクトを生成するためのインターフェースを提供するデザインパターンです。このパターンは特に、システムを具体的なクラスから独立させたい場合や、一連の製品を一貫して生成したい場合に有効です。Abstract Factory パターンを使用することで、クライアントは使用する具体的なファクトリを知ることなく、製品のファミリーを生成することができます。
---

## Table of contents

## パターンの概要

このパターンは以下の主要なコンポーネントで構成されます：

1. **Abstract Factory**: 個々の製品のファミリーを生成するためのインターフェースを定義します。
2. **Concrete Factory**: Abstract Factory インターフェースを実装し、具体的な製品のインスタンスを生成します。
3. **Abstract Product**: 製品オブジェクトのインターフェースを定義します。
4. **Concrete Product**: 具体的な製品を表すクラス。これらは Concrete Factory によって生成されます。
5. **Client**: Abstract Factory と Abstract Product のインターフェースを使用して、製品のファミリーを操作します。

## Abstract Factory パターンの利点

- **依存性の分離**: クライアントは具体的な製品のクラスから独立して操作が可能です。
- **製品ファミリーの統合性**: 同じ製品ファミリーのオブジェクト群が一貫して生成されることを保証します。
- **拡張性**: 新しい種類の製品をファクトリに追加することが容易です。

## 実装例

```java
// Abstract Factory
interface FurnitureFactory {
    Chair createChair();
    Sofa createSofa();
}

// Concrete Factory
class ModernFurnitureFactory implements FurnitureFactory {
    @Override
    public Chair createChair() {
        return new ModernChair();
    }

    @Override
    public Sofa createSofa() {
        return new ModernSofa();
    }
}

// Abstract Product
interface Chair {
    void describe();
}

// Concrete Product
class ModernChair implements Chair {
    @Override
    public void describe() {
        System.out.println("This is a modern chair.");
    }
}

interface Sofa {
    void describe();
}

class ModernSofa implements Sofa {
    @Override
    public void describe() {
        System.out.println("This is a modern sofa.");
    }
}

// Client
public class FurnitureStore {
    private Chair chair;
    private Sofa sofa;

    public FurnitureStore(FurnitureFactory factory) {
        chair = factory.createChair();
        sofa = factory.createSofa();
    }

    public void describeFurniture() {
        chair.describe();
        sofa.describe();
    }
}

public class Demo {
    public static void main(String[] args) {
        FurnitureFactory factory = new ModernFurnitureFactory();
        FurnitureStore store = new FurnitureStore(factory);
        store.describeFurniture();
    }
}
```

## 関連記事

Abstract Factory パターンについてさらに学びたい場合は、以下のリソースが役立ちます。

1. **Refactoring Guru** - [Abstract Factory](https://refactoring.guru/design-patterns/abstract-factory)

   - この記事では、Abstract Factory パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Abstract Factory Design Pattern](https://sourcemaking.com/design_patterns/abstract_factory)
   - Abstract Factory パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介しています。
