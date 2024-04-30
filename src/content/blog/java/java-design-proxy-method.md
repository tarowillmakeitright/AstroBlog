---
author: Taro Gray
pubDatetime: 2024-04-27T14:08:00.00Z
title: Java Design Pattern Proxy Method について
postSlug: java-design-proxy-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Proxy Method
description: Proxy パターンは、あるオブジェクトへのアクセスを制御するための代理（プロキシ）オブジェクトを提供するデザインパターンです。このパターンを利用することで、オブジェクトの作成のコストが高い場合の遅延初期化、アクセス制御、ロギング、キャッシングなど、様々な目的で利用できます。
---

## Table of contents

### パターンの構成要素

1. **Subject**: RealSubject と Proxy が共通で実装するインターフェース。
2. **RealSubject**: 実際のオブジェクトで、クライアントが利用したい本物のサービスまたはリソース。
3. **Proxy**: RealSubject の代理として機能するオブジェクト。クライアントからの要求を受け、必要に応じて RealSubject にその要求を転送し、その結果をクライアントに返します。

## Proxy パターンの利点

- **セキュリティ**: オブジェクトへのアクセス制御を提供し、不正なアクセスやリソースの誤用を防ぎます。
- **遅延初期化**: 実際のオブジェクトのインスタンス化を遅らせることができ、リソースを効率的に利用できます。
- **透過的なロギング**: メソッド呼び出しを透過的にログに記録することができ、デバッグや監査に役立ちます。

## 実装例

```java
// Subject interface
interface Image {
    void display();
}

// RealSubject
class RealImage implements Image {
    private String fileName;

    public RealImage(String fileName) {
        this.fileName = fileName;
        loadFromDisk(fileName);
    }

    @Override
    public void display() {
        System.out.println("Displaying " + fileName);
    }

    private void loadFromDisk(String fileName) {
        System.out.println("Loading " + fileName);
    }
}

// Proxy
class ProxyImage implements Image {
    private RealImage realImage;
    private String fileName;

    public ProxyImage(String fileName) {
        this.fileName = fileName;
    }

    @Override
    public void display() {
        if (realImage == null) {
            realImage = new RealImage(fileName);
        }
        realImage.display();
    }
}

// Client
public class ProxyDemo {
    public static void main(String[] args) {
        Image image = new ProxyImage("test_10mb.jpg");

        // Image will be loaded from disk
        image.display();
        // Image will not be loaded from disk
        image.display();
    }
}
```

## 関連記事

Proxy パターンについてさらに学びたい場合は、以下の記事が役立ちます：

1. **Refactoring Guru** - [Proxy Pattern](https://refactoring.guru/design-patterns/proxy)

   - この記事では、Proxy パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Proxy Design Pattern](https://sourcemaking.com/design_patterns/proxy)
   - Proxy パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介しています。
