---
author: Taro Gray
pubDatetime: 2024-04-27T13:50:00.00Z
title: Java Design Pattern Flyweight Method について
postSlug: java-design-flyweight-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Flyweight Method
description: Flyweight パターンは、多数の細かなオブジェクトを効率的に共有させることで、メモリ使用量を削減するデザインパターンです。特に、大量の類似オブジェクトが必要とされる場合に、重複を最小限に抑えることでシステムリソースの消費を抑えます。
---

## Table of contents

## パターンの構成要素

1. **Flyweight**: 再利用可能なオブジェクトの振る舞いを定義します。内部状態（Intrinsic state）はオブジェクト間で共有され、外部状態（Extrinsic state）はコンテキストごとに異なります。
2. **ConcreteFlyweight**: Flyweight インターフェースを実装し、内部状態を持つ具体的なクラスです。
3. **Flyweight Factory**: Flyweight オブジェクトの生成と管理を担います。既に生成されたインスタンスがある場合はそれを返し、ない場合は新たに作成します。
4. **Client**: Flyweight オブジェクトを利用し、外部状態を保持します。

## Flyweight パターンの利点

- **メモリ効率の向上**: 大量のオブジェクトを生成する必要がある場面でメモリ消費を抑えることができます。
- **パフォーマンスの向上**: オブジェクトのインスタンス化数が減ることで、起動時間の短縮やランタイムパフォーマンスの向上が見込まれます。

## 実装例

```java
// Flyweight interface
interface CoffeeOrder {
    void serveCoffee(CoffeeOrderContext context);
}

// ConcreteFlyweight
class CoffeeFlavor implements CoffeeOrder {
    private final String flavor;

    public CoffeeFlavor(String flavor) {
        this.flavor = flavor;
    }

    public void serveCoffee(CoffeeOrderContext context) {
        System.out.println("Serving " + flavor + " to table " + context.getTable());
    }
}

// Context
class CoffeeOrderContext {
    private final int tableNumber;

    public CoffeeOrderContext(int tableNumber) {
        this.tableNumber = tableNumber;
    }

    public int getTable() {
        return tableNumber;
    }
}

// Flyweight Factory
class CoffeeFlavorFactory {
    private Map<String, CoffeeFlavor> flavors = new HashMap<>();

    public CoffeeFlavor getCoffeeFlavor(String flavorName) {
        CoffeeFlavor flavor = flavors.get(flavorName);
        if (flavor == null) {
            flavor = new CoffeeFlavor(flavorName);
            flavors.put(flavorName, flavor);
        }
        return flavor;
    }

    public int getTotalCoffeeFlavorsMade() {
        return flavors.size();
    }
}

// Client
public class FlyweightDemo {
    private final static CoffeeFlavorFactory flavorFactory = new CoffeeFlavorFactory();

    public static void main(String[] args) {
        CoffeeOrderContext table1 = new CoffeeOrderContext(1);
        CoffeeOrderContext table2 = new CoffeeOrderContext(2);

        serveCoffee("Cappuccino", table1);
        serveCoffee("Cappuccino", table2);
        serveCoffee("Espresso", table1);

        System.out.println("Total Coffee flavors made: " + flavorFactory.getTotalCoffeeFlavorsMade());
    }

    public static void serveCoffee(String flavorName, CoffeeOrderContext context) {
        CoffeeFlavor flavor = flavorFactory.getCoffeeFlavor(flavorName);
        flavor.serveCoffee(context);
    }
}
```

## 関連記事

Flyweight パターンについてさらに学びたい場合は、以下の記事が役立ちます：

1. **Refactoring Guru** - [Flyweight Pattern](https://refactoring.guru/design-patterns/flyweight)
   - この記事では、Flyweight パターンの詳細な説明、利点、欠点、さらには多言語で

の実装例が提供されています。

2. **SourceMaking** - [Flyweight Design Pattern](https://sourcemaking.com/design_patterns/flyweight)
   - Flyweight パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介しています。
