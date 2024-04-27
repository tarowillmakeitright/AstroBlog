---
author: Taro Gray
pubDatetime: 2024-04-26T22:37:00.00Z
title: Java Design Pattern Builder Method について
postSlug: java-design-builder-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Builder Method
description: Builder パターンは、複雑なオブジェクトの構築を簡素化するためのデザインパターンです。このパターンは、特にオブジェクトの構成が多段階にわたる場合や、多くの構成要素を含むオブジェクトの生成が必要な場合に役立ちます。Builder パターンを使用することで、最終オブジェクトの表現を生成するコードから分離することができ、同じ構築プロセスで異なる表現を生成できるようになります。
---

## Table of contents

## Builder パターンの概要

このパターンは、複数の簡単なオブジェクトから1つの複合オブジェクトを段階的に構築する方法を提供します。主に以下の4つのコンポーネントから構成されます：

1. **Builder**: 生成するオブジェクトの構成要素を作成するためのインターフェース。
2. **ConcreteBuilder**: Builder インターフェースの実装クラスで、オブジェクトの部品を構築し、構築過程でオブジェクトを組み立てます。
3. **Director**: 構築のプロセスを制御し、Builder インターフェースを使用してオブジェクトを構築します。
4. **Product**: 最終的なオブジェクト。ConcreteBuilder によって構築されます。

## Builder パターンの利点

- **複雑性の分離**: クライアントは具体的な構築プロセスを知る必要がなく、Director がプロセスを管理します。
- **詳細な制御**: 構築プロセスの各ステップを細かく制御できるため、最終的なオブジェクトがクライアントのニーズに正確に合わせることができます。
- **再利用性**: Builder インターフェースを異なる具体的な実装で再利用することが可能です。

## 実装例

Java での Builder パターンの例を以下に示します。

```java
// Product
class Car {
    private String wheels;
    private String engine;
    private String body;

    public void setWheels(String wheels) {
        this.wheels = wheels;
    }

    public void setEngine(String engine) {
        this.engine = engine;
    }

    public void setBody(String body) {
        this.body = body;
    }
}

// Builder
interface CarBuilder {
    void buildWheels();
    void buildEngine();
    void buildBody();
    Car getCar();
}

// ConcreteBuilder
class FerrariBuilder implements CarBuilder {
    private Car car;

    public FerrariBuilder() {
        this.car = new Car();
    }

    @Override
    public void buildWheels() {
        car.setWheels("Sports wheels");
    }

    @Override
    public void buildEngine() {
        car.setEngine("V8 engine");
    }

    @Override
    public void buildBody() {
        car.setBody("Sports body");
    }

    @Override
    public Car getCar() {
        return car;
    }
}

// Director
class CarDirector {
    private CarBuilder builder;

    public CarDirector(CarBuilder builder) {
        this.builder = builder;
    }

    public void constructCar() {
        builder.buildBody();
        builder.buildEngine();
        builder.buildWheels();
    }

    public Car getCar() {
        return builder.getCar();
    }
}

// Main
public class BuilderDemo {
    public static void main(String[] args) {
        CarBuilder builder = new FerrariBuilder();
        CarDirector director = new CarDirector(builder);
        director.constructCar();
        Car car = director.getCar();
    }
}
```

## 関連記事

Builder Method パターンについてより深く理解するための参考資料を以下に示します。

1. **Refactoring Guru** - [Builder Method](https://refactoring.guru/design-patterns/builder-method)

   - このサイトでは、Builder Method パターンについて詳細な説明と、多言語での実装例が提供されています。

2. **SourceMaking** - [Builder Method Design Pattern](https://sourcemaking.com/design_patterns/builder_method)
   - パターンの動機、構造、そして具体的な使用例について詳しく説明されており、実際のアプリケーションでの適用例も紹介されています。
