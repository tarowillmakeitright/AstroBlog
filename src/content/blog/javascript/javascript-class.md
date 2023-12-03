---
author: Taro Gray
pubDatetime: 2023-12-03T04:46:00.007Z
title: JavaScriptクラスの魔法：公開・非公開プロパティとメソッド
postSlug: javascript-class-public-private
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Javascript
description: JavaScriptのクラスは、公開（public）、非公開（private）プロパティやメソッド、さらにはgetter、setter、staticなど、様々な機能を備えています。この記事では、これらの機能を使った面白くて実用的なコード例を紹介します。
---

## Table of contents

## JavaScriptクラスの魔法：公開・非公開プロパティとメソッド

JavaScriptのクラスは、公開（public）、非公開（private）プロパティやメソッド、さらにはgetter、setter、staticなど、様々な機能を備えています。この記事では、これらの機能を使った面白くて実用的なコード例を紹介します。

## 1. シンプルなクラスの例

まずは基本から。シンプルなクラスの例を見てみましょう。

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  speak() {
    console.log(`${this.name} makes a noise.`);
  }
}

const dog = new Animal("Rex");
dog.speak(); // Rex makes a noise.
```

## 2. Private プロパティとメソッド

JavaScriptでは、`#`記号を使ってプライベートプロパティやメソッドを宣言できます。

```javascript
class SecretAgent {
  #password;

  constructor(password) {
    this.#password = password;
  }

  #decrypt() {
    // パスワードを復号化するロジック
    return "Decrypted Secret";
  }

  revealSecret() {
    return this.#decrypt();
  }
}

const agent = new SecretAgent("supersecret");
console.log(agent.revealSecret()); // Decrypted Secret
```

この例では、`#password`と`#decrypt`メソッドは外部からアクセスできません。

## 3. Getter と Setter

getterとsetterは、プロパティの値を読み書きするための特別なメソッドです。

```javascript
class Temperature {
  constructor(celsius) {
    this.celsius = celsius;
  }

  get fahrenheit() {
    return this.celsius * 1.8 + 32;
  }

  set fahrenheit(value) {
    this.celsius = (value - 32) / 1.8;
  }
}

const temp = new Temperature(30);
console.log(temp.fahrenheit); // 86
temp.fahrenheit = 50;
console.log(temp.celsius); // 10
```

## 4. Static メソッド

staticメソッドは、インスタンスではなくクラス自体に属しています。

```javascript
class Calculator {
  static add(a, b) {
    return a + b;
  }
}

console.log(Calculator.add(5, 3)); // 8
```

## 5. 面白い例：ハッカーのクラス

面白い例を一つ。ハッカーのクラスを作ってみましょう！

```javascript
class Hacker {
  static hack() {
    console.log("You've been hacked!");
  }
}

Hacker.hack(); // You've been hacked!
```

このクラスは、ハッカーの典型的な行動をシンプルに表現しています。もちろん、実際のハッキングには使わないでくださいね！
これらの例がJavaScriptのクラスの様々な機能を理解するのに役立つことを願っています。楽しんで学んでください！
