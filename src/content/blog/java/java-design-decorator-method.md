---
author: Taro Gray
pubDatetime: 2024-04-27T12:31:00.00Z
title: Java Design Pattern Decorator Method について
postSlug: java-design-decorator-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Decorator Method
description: Decorator パターンは、オブジェクトに動的に新しい機能を追加するためのデザインパターンです。このパターンは、サブクラス化の代わりに機能を拡張する柔軟な方法を提供し、オブジェクトの機能をランタイムに拡張することが可能です。特に、システムの設計が閉じていて拡張が難しい場合に有効です。
---

## Table of contents

## パターンの概要

Decorator パターンは以下の主要なコンポーネントから構成されます：

1. **Component**: オブジェクトのインターフェースを定義します。デコレータと具体的なコンポーネントはこのインターフェースを実装します。
2. **ConcreteComponent**: Component インターフェースを実装し、基本的な機能を提供するクラスです。
3. **Decorator**: Component インターフェースを実装し、持っている Component オブジェクトをラップします。これにより、追加機能を提供します。
4. **ConcreteDecorator**: Decorator クラスを実装し、Component に新しい機能を追加します。

## Decorator パターンの利点

- **拡張性**: 新しいデコレータを追加することで、既存のコードを変更することなく機能を拡張できます。
- **柔軟性**: 装飾を動的に追加または削除して、システムの振る舞いをランタイムで変更できます。
- **代替継承**: 多重継承の複雑さを避けながら、機能を追加できます。

## 実装例

```java
// Component
interface Coffee {
    String getDescription();
    double getCost();
}

// ConcreteComponent
class SimpleCoffee implements Coffee {
    public String getDescription() {
        return "Simple Coffee";
    }

    public double getCost() {
        return 1.0;
    }
}

// Decorator
abstract class CoffeeDecorator implements Coffee {
    protected Coffee decoratedCoffee;

    public CoffeeDecorator(Coffee coffee) {
        this.decoratedCoffee = coffee;
    }

    public String getDescription() {
        return decoratedCoffee.getDescription();
    }

    public double getCost() {
        return decoratedCoffee.getCost();
    }
}

// ConcreteDecorator
class MilkDecorator extends CoffeeDecorator {
    public MilkDecorator(Coffee coffee) {
        super(coffee);
    }

    @Override
    public String getDescription() {
        return super.getDescription() + ", milk";
    }

    @Override
    public double getCost() {
        return super.getCost() + 0.5;
    }
}

// Client
public class DecoratorDemo {
    public static void main(String[] args) {
        Coffee coffee = new SimpleCoffee();
        System.out.println(coffee.getDescription() + " Cost: $" + coffee.getCost());

        Coffee milkCoffee = new MilkDecorator(new SimpleCoffee());
        System.out.println(milkCoffee.getDescription() + " Cost: $" + milkCoffee.getCost());
    }
}
```

## 関連記事

Decorator パターンについてさらに学びたい場合は、以下の記事が役立ちます。

1. **Refactoring Guru** - [Decorator Pattern](https://refactoring.guru/design-patterns/decorator)

   - この記事では、Decorator パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Decorator Design Pattern](https://sourcemaking.com/design_patterns/decorator)
   - Decorator パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介しています。

これらの記事を通じて、Decorator

## 関連記事

Decorator パターンに関してさらに詳しく学びたい場合は、以下の記事が役立ちます。

1. **Refactoring Guru** - [Decorator Pattern](https://refactoring.guru/design-patterns/decorator)

   - この記事では、Decorator パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Decorator Design Pattern](https://sourcemaking.com/design_patterns/decorator)
   - Decorator パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介
