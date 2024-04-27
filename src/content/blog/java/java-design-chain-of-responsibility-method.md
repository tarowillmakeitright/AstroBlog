---
author: Taro Gray
pubDatetime: 2024-04-27T12:46:00.00Z
title: Java Design Pattern Chain of Responsibility Method について
postSlug: java-design-chain-of-responsibility-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Chain of Responsibility Method
description: Chain of Responsibility パターンは、複数のオブジェクトのチェーンを通じてリクエストを処理する方法を提供するデザインパターンです。このパターンは、リクエストを処理できる最初のオブジェクトがそれを受け取り、処理します。この方法は、コマンドオブジェクトを一連の処理ユニットに順次渡すことにより、オブジェクト間の結合を減少させることができます。
---

## Table of contents

## パターンの概要

Chain of Responsibility パターンは主に以下のコンポーネントで構成されます：

1. **Handler**: リクエストを処理するインターフェースを定義します。次のハンドラへのリファレンスも保持します。
2. **ConcreteHandler**: Handler インターフェースを実装し、リクエストを処理する具体的な方法を提供します。処理できない場合は、リクエストをチェーンの次のオブジェクトに渡します。
3. **Client**: チェーンの最初のハンドラにリクエストを送信します。

## Chain of Responsibility パターンの利点

- **低い結合度**: リクエストの送り手と受け手が互いに独立しているため、オブジェクト間の結合度が低くなります。
- **動的な再配置**: リクエストを処理するオブジェクトのチェーンを動的に変更することが可能です。
- **責任の分散**: リクエストを処理する責任を複数のオブジェクトに分散させることができます。

## 実装例

```java
// Handler
abstract class Handler {
    protected Handler successor;

    public void setSuccessor(Handler successor) {
        this.successor = successor;
    }

    public abstract void handleRequest(String request);
}

// ConcreteHandler1
class ConcreteHandler1 extends Handler {
    public void handleRequest(String request) {
        if (request.equals("One")) {
            System.out.println("One handled by ConcreteHandler1");
        } else if (successor != null) {
            successor.handleRequest(request);
        }
    }
}

// ConcreteHandler2
class ConcreteHandler2 extends Handler {
    public void handleRequest(String request) {
        if (request.equals("Two")) {
            System.out.println("Two handled by ConcreteHandler2");
        } else if (successor != null) {
            successor.handleRequest(request);
        }
    }
}

// Client
public class ChainDemo {
    public static void main(String[] args) {
        Handler h1 = new ConcreteHandler1();
        Handler h2 = new ConcreteHandler2();

        h1.setSuccessor(h2);

        h1.handleRequest("Two");
        h1.handleRequest("One");
    }
}
```

## 関連記事

Chain of Responsibility パターンについてさらに学びたい場合は、以下の記事が役立ちます：

1. **Refactoring Guru** - [Chain of Responsibility](https://refactoring.guru/design-patterns/chain-of-responsibility)

   - この記事では、Chain of Responsibility パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Chain of Responsibility Design Pattern](https://sourcemaking.com/design_patterns/chain_of_responsibility)
   - Chain of Responsibility パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介しています。
