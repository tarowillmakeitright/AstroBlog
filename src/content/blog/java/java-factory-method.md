---
author: Taro Gray
pubDatetime: 2024-04-26T15:15:00.00Z
title: Factory Method パターンの解説
Factory Method パターンの解説
postSlug: java-template-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Design Pattern
  - Template Method Pattern
description: Factory Method パターンは、デザインパターンの一つで、インスタンスの生成をサブクラスに委譲することで、システムの柔軟性と拡張性を高める手法です。このパターンは特に、クライアントとクラスの具体的な実装の間の結合度を低減する場合に有効です。
---

## Table of contents

## Factory Method パターンの解説

Factory Method パターンは、デザインパターンの一つで、インスタンスの生成をサブクラスに委譲することで、システムの柔軟性と拡張性を高める手法です。このパターンは特に、クライアントとクラスの具体的な実装の間の結合度を低減する場合に有効です。

## パターンの概要

Factory Method パターンは、オブジェクトの作成に関する責任を持つインターフェースを定義しますが、どのクラスのインスタンスを作成するかについては、サブクラスが決定します。これにより、クラスのインスタンス生成をクラスの内部にカプセル化することができ、クライアントは具体的なクラスに依存することなくオブジェクトを生成できます。

## 基本的な構造

1. **Product** - 生成するオブジェクトのインターフェースまたは抽象クラス。
2. **ConcreteProduct** - `Product` インターフェースを実装する具体的なクラス。
3. **Creator** - `Product` オブジェクトを返す抽象メソッドを持つクラス。
4. **ConcreteCreator** - `Creator` クラスを継承し、具体的な `Product` インスタンスを生成するメソッドをオーバーライドするクラス。

## コード例

```java
// Product
public abstract class Dialog {
    public void render() {
        Button okButton = createButton();
        okButton.onClick(() -> System.out.println("Dialog OK clicked"));
        okButton.render();
    }

    public abstract Button createButton();
}

// ConcreteProduct
public class WindowsButton implements Button {
    public void render() {
        System.out.println("Render a Windows button");
    }

    public void onClick(Runnable action) {
        action.run();
    }
}

// Creator
public class WindowsDialog extends Dialog {
    @Override
    public Button createButton() {
        return new WindowsButton();
    }
}

// Main class to use Factory Method
public class Client {
    public static void main(String[] args) {
        Dialog dialog = new WindowsDialog();
        dialog.render();
    }
}
```

## 関連記事

Factory Method パターンについてより深く理解するための参考資料を以下に示します。

1. **Refactoring Guru** - [Factory Method](https://refactoring.guru/design-patterns/factory-method)

   - このサイトでは、Factory Method パターンについて詳細な説明と、多言語での実装例が提供されています。

2. **SourceMaking** - [Factory Method Design Pattern](https://sourcemaking.com/design_patterns/factory_method)
   - パターンの動機、構造、そして具体的な使用例について詳しく説明されており、実際のアプリケーションでの適用例も紹介されています。
