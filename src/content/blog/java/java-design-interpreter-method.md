---
author: Taro Gray
pubDatetime: 2024-04-27T14:24:00.00Z
title: Java Design Pattern Interpreter Method について
postSlug: java-design-interpreter-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Interpreter Method
description: Interpreter パターンは、特定のプログラミング言語の文法に対して解釈器を提供するデザインパターンです。このパターンは、文法が比較的単純で、効率が最も重要でない場合に適しています。多くの場合、コンパイラやインタープリタ、プログラミング言語の解析ツールで使用されます。
---

## Table of contents

## パターンの構成要素

1. **Abstract Expression**: 文法のルールを表すすべてのノード共通のインターフェース。
2. **Terminal Expression**: 文法の終端記号に対応するクラス。
3. **Nonterminal Expression**: 文法の非終端記号を表すクラスで、他の Expression インターフェースの実装を組み合わせて規則を定義します。
4. **Context**: 解釈器が文法を解釈するために必要な情報を含んでいます。
5. **Client**: Interpreter パターンの構造を使用して特定の文を解釈します。

## Interpreter パターンの利点

- **拡張性**: 新しい解釈規則を簡単に追加できます。
- **再利用性**: 既存の文法規則を新しい文脈で再利用することができます。
- **分離と管理**: 文法の規則を個別のクラスに分離することで、文法が複雑になっても管理しやすくなります。

## 実装例

以下は、簡単な算術式を解釈するための Interpreter パターンの Java 実装例です。

```java
// Abstract Expression
interface Expression {
    int interpret(Context context);
}

// Terminal Expression
class Number implements Expression {
    private int number;

    public Number(int number) {
        this.number = number;
    }

    @Override
    public int interpret(Context context) {
        return number;
    }
}

// Nonterminal Expression
class Plus implements Expression {
    private Expression leftOperand;
    private Expression rightOperand;

    public Plus(Expression left, Expression right) {
        this.leftOperand = left;
        this.rightOperand = right;
    }

    @Override
    public int interpret(Context context) {
        return leftOperand.interpret(context) + rightOperand.interpret(context);
    }
}

class Minus implements Expression {
    private Expression leftOperand;
    private Expression rightOperand;

    public Minus(Expression left, Expression right) {
        this.leftOperand = left;
        this.rightOperand = right;
    }

    @Override
    public int interpret(Context context) {
        return leftOperand.interpret(context) - rightOperand.interpret(context);
    }
}

// Context (Optional for simple example)
class Context {
}

// Client
public class InterpreterDemo {
    public static void main(String[] args) {
        Expression isMinus = new Minus(new Number(10), new Number(5));
        Expression isPlus = new Plus(isMinus, new Number(2));

        System.out.println("10 - 5 + 2 = " + isPlus.interpret(new Context()));
    }
}
```

## 関連記事

Interpreter パターンについてさらに学びたい場合は、以下の記事が役立ちます：

1. **Refactoring Guru** - [Interpreter Pattern](https://refactoring.guru/design-patterns/interpreter)

   - この記事では、Interpreter パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Interpreter Design Pattern](https://sourcemaking.com/design_patterns/interpreter)
   - Interpreter パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介しています。
