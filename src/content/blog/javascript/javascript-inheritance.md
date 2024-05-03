---
author: Taro Gray
pubDatetime: 2024-05-03T12:34:00.00Z
title: JavaScriptにおける継承とコンポジションの解説
postSlug: javascript-inheritance
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Javascript
  - asynchronous-API
description: JavaScriptの設計において、継承とコンポジションはオブジェクト間の関係を定義するための二つの主要な方法です。このブログ記事では、それぞれの概念を具体的な例を交えて解説し、いつどのように使い分けるべきかを考察します。
---

## Table of contents

## 継承: 「私はアニマルです」

継承は、あるクラス（サブクラス）が別のクラス（スーパークラス）の特性を引き継ぐオブジェクト指向の概念です。これにより、コードの再利用性が向上し、関連するクラス間で機能を共有できます。

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  identify() {
    console.log(`私は${this.name}です。`);
  }
}

class Dog extends Animal {
  constructor(name) {
    super(name);
  }
}

const dog = new Dog("犬");
dog.identify(); // "私は犬です。"
```

この例では、`Dog`クラスが`Animal`クラスから`name`プロパティと`identify`メソッドを継承しています。`Dog`は`Animal`の特性を「引き継ぐ」ことで、`Animal`の定義をそのまま利用しています。

## コンポジション: 「私はアニマルの要素です」

コンポジションは、一つのオブジェクトが他のオブジェクトの一部を保有または管理するデザインパターンです。これは「持っている（has-a）」関係とも説明され、オブジェクト間の独立性を保ちつつ機能を組み合わせることができます。

```javascript
class Animal {
  constructor(name) {
    this.name = name;
  }

  identify() {
    console.log(`私は${this.name}の要素です。`);
  }
}

class Farm {
  constructor() {
    this.animals = [];
  }

  addAnimal(animal) {
    this.animals.push(animal);
  }

  identifyAnimals() {
    this.animals.forEach(animal => animal.identify());
  }
}

const farm = new Farm();
const cow = new Animal("牛");
farm.addAnimal(cow);

farm.identifyAnimals(); // "私は牛の要素です。"
```

この例では、`Farm`クラスは多くの`Animal`オブジェクトを持っています。`Farm`はそれぞれの`Animal`の機能を利用するが、`Animal`自身の振る舞いを直接継承するわけではありません。

## 使い分けのポイント

- **継承**は、「is-a（〜である）」の関係が自然な場合に適しています。例えば、「DogはAnimalである」といったケースです。
- **コンポジション**は、より柔軟な関係を築きたい時や、継承による密結合を避けたい場合に有効です。例えば、異なるタイプのオブジェクトを一つの集合に管理したい場合などです。

## 関連記事

1. **MDN Web Docs** - [Inheritance and the prototype chain](https://developer.mozilla.org/ja/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)  
   このMDNの記事では、JavaScriptにおける継承とプロトタイプチェーンについて詳細に解説しています。プロトタイプベースの継承がどのように機能するかを理解するのに役立ちます。

2. **JavaScript Info** - [Composition over inheritance](https://javascript.info/mixins)  
   「継承よりコンポジション」というコンセプトに焦点を当てたこの記事では、JavaScriptにおけるミックスイン（mixin）というテクニックを通じて、コンポジションをどのように活用できるかを示しています。

3. **Composition vs Inheritance: How to Choose?** - [Smashing Magazine](https://www.smashingmagazine.com/2016/08/choosing-the-right-approach-to-web-animation/)  
   このSmashing Magazineの記事はアニメーションを例にしていますが、コンポジションと継承の概念を選択する際のガイドラインを提供しています。アプローチの違いを理解するのに役立ちます。
