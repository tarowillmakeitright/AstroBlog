---
author: Taro Gray
pubDatetime: 2024-04-27T12:15:00.00Z
title: Java Design Pattern Composite Method について
postSlug: java-design-composite-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Composite Method
description:
---

## Table of contents

## Composite パターンの詳細解説

Composite パターンは、オブジェクトを木構造で表し、個別のオブジェクトとオブジェクトのコンポジションをクライアントが同一の方法で扱えるようにするデザインパターンです。このパターンは、部分-全体の階層を持つオブジェクト群を扱う際に特に有効で、クライアントが単一オブジェクトと複合オブジェクトを同一視して扱えるようにします。

## パターンの概要

Composite パターンは以下の3つの主要なコンポーネントで構成されます：

1. **Component**: 全てのオブジェクトの共通のインターフェース。個別オブジェクトとコンポジットオブジェクトがこのインターフェースを実装します。
2. **Leaf**: Component インターフェースの具体的な実装で、子を持たないコンポーネントを表します。
3. **Composite**: Component インターフェースを実装し、子コンポーネントのリストを持つクラス。子を管理（追加、削除）する方法を提供します。

## Composite パターンの利点

- **統一されたインターフェース**: オブジェクトのコレクションと単一オブジェクトをクライアントが同じように扱える。
- **簡便な構造管理**: オブジェクトの階層を簡単に追加・削除する操作が可能。
- **柔軟性の向上**: 新しい種類のコンポーネントを容易に追加できる。

## 実装例

```java
// Component
interface Graphic {
    void draw();
}

// Leaf
class Line implements Graphic {
    public void draw() {
        System.out.println("Draw a line");
    }
}

class Text implements Graphic {
    public void draw() {
        System.out.println("Draw a text");
    }
}

// Composite
class CompositeGraphic implements Graphic {
    private List<Graphic> children = new ArrayList<>();

    public void add(Graphic graphic) {
        children.add(graphic);
    }

    public void remove(Graphic graphic) {
        children.remove(graphic);
    }

    public void draw() {
        for (Graphic graphic : children) {
            graphic.draw();
        }
    }
}

// Client
public class CompositeDemo {
    public static void main(String[] args) {
        CompositeGraphic graphic = new CompositeGraphic();
        graphic.add(new Line());
        graphic.add(new Text());

        graphic.draw();
    }
}
```

## 関連記事

Composite パターンについてさらに詳しく学びたい場合は、以下の記事が役立ちます。

1. **Refactoring Guru** - [Composite Pattern](https://refactoring.guru/design-patterns/composite)

   - この記事では、Composite パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Composite Design Pattern](https://sourcemaking.com/design_patterns/composite)
   - Composite パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介しています。
