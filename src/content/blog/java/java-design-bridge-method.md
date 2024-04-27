---
author: Taro Gray
pubDatetime: 2024-04-27T11:59:00.00Z
title: Java Design Pattern Bridge Method について
postSlug: java-design-bridge-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Bridge Method
description: Bridge パターンは、抽象化と実装を分離し、それらが独立に変化できるようにするデザインパターンです。このパターンは特に、システムの抽象化部分と実装部分が多岐にわたって拡張される可能性がある場合に有効です。Bridge パターンを用いることで、クライアントのコードを変更することなく新しい実装を容易に追加することができます。
---

## Table of contents

## パターンの構成

Bridge パターンは主に以下の4つのコンポーネントで構成されます：

1. **Abstraction（抽象化）**: 高レベルの制御ロジックを提供するインターフェース。このクラスは実装部分を持つ Implementor オブジェクトを参照します。
2. **Refined Abstraction（洗練された抽象化）**: Abstraction を拡張して新たな機能を実装します。
3. **Implementor（実装者）**: 実装クラスのインターフェースを定義します。
4. **ConcreteImplementor（具体的な実装者）**: Implementor インターフェースの具体的な実装を提供します。

## Bridge パターンの利点

- **拡張性**: 抽象化と実装を独立に拡張することが可能です。
- **柔軟性**: 新しい実装を追加することが、既存のクライアントコードに影響を与えることなく可能です。
- **詳細の隠蔽**: 実装の詳細がクライアントから隠され、API の使用がシンプルになります。

## 実装例

```java
// Implementor
interface DrawingAPI {
    void drawCircle(double x, double y, double radius);
}

// ConcreteImplementor
class DrawingAPI1 implements DrawingAPI {
    public void drawCircle(double x, double y, double radius) {
        System.out.printf("API1.circle at %f:%f radius %f\n", x, y, radius);
    }
}

class DrawingAPI2 implements DrawingAPI {
    public void drawCircle(double x, double y, double radius) {
        System.out.printf("API2.circle at %f:%f radius %f\n", x, y, radius);
    }
}

// Abstraction
abstract class Shape {
    protected DrawingAPI drawingAPI;

    protected Shape(DrawingAPI drawingAPI){
        this.drawingAPI = drawingAPI;
    }
    public abstract void draw(); // low-level
    public abstract void resizeByPercentage(double pct); // high-level
}

// RefinedAbstraction
class CircleShape extends Shape {
    private double x, y, radius;

    public CircleShape(double x, double y, double radius, DrawingAPI drawingAPI) {
        super(drawingAPI);
        this.x = x;
        this.y = y;
        this.radius = radius;
    }

    public void draw() {
        drawingAPI.drawCircle(x, y, radius);
    }

    public void resizeByPercentage(double pct) {
        radius *= pct;
    }
}

// Client
public class BridgePatternDemo {
    public static void main(String[] args) {
        Shape[] shapes = new Shape[] {
            new CircleShape(1, 2, 3, new DrawingAPI1()),
            new CircleShape(5, 7, 11, new DrawingAPI2()),
        };

        for (Shape shape : shapes) {
            shape.resizeByPercentage(2.5);
            shape.draw();
        }
    }
}
```

## 関連記事

Bridge パターンについてさらに学びたい場合は、以下のリソースが役立ちます：

1. **Refactoring Guru** - [Bridge](https://refactoring.guru/design-patterns/bridge)
   - この記事では、Bridge パターンの詳細な説明、利点、欠点、さらには多言語での

実装例が提供されています。

2. **SourceMaking** - [Bridge Design Pattern](https://sourcemaking.com/design_patterns/bridge)
   - Bridge パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介しています。
