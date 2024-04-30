---
author: Taro Gray
pubDatetime: 2024-04-27T12:37:00.00Z
title: Java Design Pattern Visitor Method について
postSlug: java-design-visitor-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Visitor Method
description: Visitor パターンは、オブジェクトの構造と処理を分離し、構造内の各要素に対して特定の操作を行うことができるデザインパターンです。このパターンは、オブジェクト構造のクラスに変更を加えずに新しい操作を簡単に追加できるという点で非常に有効です。特に、異なる型の要素に対して異なる操作を行う必要がある複雑なオブジェクトコレクションを扱う場合に適しています。
---

## Table of contents

## パターンの概要

Visitor パターンは以下の主要なコンポーネントから構成されます：

1. **Visitor**: 操作を実行するためのインターフェース。具体的な訪問者がこのインターフェースを実装します。
2. **ConcreteVisitor**: Visitor インターフェースを実装し、異なるタイプの要素に対して具体的な操作を定義します。
3. **Element**: 要素を表すインターフェースで、訪問者を受け入れる `accept` メソッドを提供します。
4. **ConcreteElement**: Element インターフェースを実装し、具体的な要素を表します。
5. **ObjectStructure**: Element オブジェクトの集合を管理し、訪問者に対してこれらの要素を提供します。

## Visitor パターンの利点

- **拡張性**: 新しい操作を既存のオブジェクト構造に簡単に追加できます。
- **分離と組織化**: データ構造と操作を分離することで、より整理されたコードが可能になります。
- **再利用性**: 訪問者は、異なるデータ構造間で共有されることがあります。

## 実装例

```java
// Element interface
interface Element {
    void accept(Visitor visitor);
}

// Concrete Element
class ConcreteElementA implements Element {
    public void accept(Visitor visitor) {
        visitor.visitConcreteElementA(this);
    }
    public String operationA() {
        return "Element A";
    }
}

class ConcreteElementB implements Element {
    public void accept(Visitor visitor) {
        visitor.visitConcreteElementB(this);
    }
    public String operationB() {
        return "Element B";
    }
}

// Visitor interface
interface Visitor {
    void visitConcreteElementA(ConcreteElementA element);
    void visitConcreteElementB(ConcreteElementB element);
}

// Concrete Visitor
class ConcreteVisitor implements Visitor {
    public void visitConcreteElementA(ConcreteElementA element) {
        System.out.println("Visiting " + element.operationA());
    }
    public void visitConcreteElementB(ConcreteElementB element) {
        System.out.println("Visiting " + element.operationB());
    }
}

// Client
public class VisitorDemo {
    public static void main(String[] args) {
        List<Element> elements = new ArrayList<>();
        elements.add(new ConcreteElementA());
        elements.add(new ConcreteElementB());

        Visitor visitor = new ConcreteVisitor();
        for (Element element : elements) {
            element.accept(visitor);
        }
    }
}
```

## 関連記事

Visitor パターンに関してさらに詳しく学びたい場合は、以下の記事が役立ちます。

1. **Refactoring Guru** - [Visitor Pattern](https://refactoring.guru/design-patterns/visitor)

   - この記事では、Visitor パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Visitor Design Pattern](https://sourcemaking.com/design_patterns/visitor)
   - Visitor パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介
