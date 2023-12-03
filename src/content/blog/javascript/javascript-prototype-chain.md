---
author: Taro Gray
pubDatetime: 2023-12-03T05:55:00.007Z
title: プロトタイプチェーンの基本
postSlug: javascript-prototype-chain
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Javascript
  - prototype-chain
description: JavaScriptは、そのプロトタイプベースの継承システムを通じて、オブジェクトが他のオブジェクトのプロパティやメソッドを継承する方法を提供しています。この記事では、JavaScriptのプロトタイプチェーンの基本を面白く学びましょう！
---

## Table of contents

## JavaScriptのプロトタイプチェーン：楽しく学ぶ！

JavaScriptは、そのプロトタイプベースの継承システムを通じて、オブジェクトが他のオブジェクトのプロパティやメソッドを継承する方法を提供しています。この記事では、JavaScriptのプロトタイプチェーンの基本を面白く学びましょう！

## 1. プロトタイプチェーンの基本

JavaScriptでは、オブジェクトは別のオブジェクトのプロパティやメソッドへの参照を持つことができます。これが「プロトタイプチェーン」です。

```javascript
function Animal(name) {
  this.name = name;
}

Animal.prototype.speak = function () {
  console.log(`${this.name} makes a noise.`);
};

const dog = new Animal("Rex");
dog.speak(); // Rex makes a noise.
```

## 2. プロトタイプチェーンの拡張

プロトタイプチェーンを拡張して、新しいメソッドを追加することができます。

```javascript
Animal.prototype.eat = function () {
  console.log(`${this.name} is eating.`);
};

dog.eat(); // Rex is eating.
```

## 3. 面白い例：宇宙ハッカー

さて、面白い例を一つ。宇宙ハッカーのクラスを作ってみましょう！

```javascript
function SpaceHacker(name) {
  Animal.call(this, name);
}

SpaceHacker.prototype = Object.create(Animal.prototype);
SpaceHacker.prototype.constructor = SpaceHacker;

SpaceHacker.prototype.hack = function () {
  console.log(`${this.name} is hacking the universe!`);
};

const alien = new SpaceHacker("Zorg");
alien.speak(); // Zorg makes a noise.
alien.hack(); // Zorg is hacking the universe!
```

この例では、`SpaceHacker`が`Animal`のプロパティとメソッドを継承し、さらに新しいメソッドを追加しています。

## 4. ハッカーとプロトタイプチェーン

ハッカーがJavaScriptのプロトタイプチェーンを利用する場面も想像してみましょう。彼らは既存のオブジェクトに新しいメソッドを追加したり、既存のメソッドを書き換えたりすることで、プログラムの挙動を変えることができます。
JavaScriptのプロトタイプチェーンは強力な機能です。これを理解することで、より柔軟で再利用可能なコードを書くことができます。面白い例を通じて学んでいただければ幸いです。ハッピーハッキング！
