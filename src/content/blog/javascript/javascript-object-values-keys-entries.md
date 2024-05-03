---
author: Taro Gray
pubDatetime: 2024-05-03T18:04:00.00Z
title: JavaScriptのObject.values, Object.keys, Object.entriesメソッドの解説
postSlug: javascript-object-values-keys-entries
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Javascript
  - object values
  - object keys
  - object entries
description: JavaScriptでは、オブジェクトのデータを扱う基本的なメソッドとして`Object.values`、`Object.keys`、`Object.entries`があります。これらのメソッドはオブジェクトのプロパティを配列として取り出すのに非常に便利です。このブログ記事では、これらのメソッドの使い方と具体的な使用例を紹介します。
---

## Table of contents

JavaScriptでは、オブジェクトのデータを扱う基本的なメソッドとして`Object.values`、`Object.keys`、`Object.entries`があります。これらのメソッドはオブジェクトのプロパティを配列として取り出すのに非常に便利です。このブログ記事では、これらのメソッドの使い方と具体的な使用例を紹介します。

## Object.values()

`Object.values()`メソッドは、オブジェクト自身の列挙可能なプロパティの値を、プロパティが出現する順に配列として返します。これにより、オブジェクトの値だけを簡単に抽出できます。

```javascript
const person = {
  name: "Alice",
  age: 25,
  country: "Japan",
};

console.log(Object.values(person));
// 出力: ['Alice', 25, 'Japan']
```

この例では、`person`オブジェクトから`name`、`age`、`country`の値が配列として取得されています。

## Object.keys()

`Object.keys()`メソッドは、オブジェクトのすべての列挙可能なプロパティのキーを配列として返します。これを利用すると、オブジェクトのキーを簡単に把握できます。

```javascript
console.log(Object.keys(person));
// 出力: ['name', 'age', 'country']
```

ここで、`person`オブジェクトのキーが配列として出力されています。

## Object.entries()

`Object.entries()`メソッドは、オブジェクト自身の列挙可能なプロパティのキーと値のペアを、[キー, 値]の形式の配列として返します。これはオブジェクトのデータをキーと値のペアとして操作したい場合に特に便利です。

```javascript
console.log(Object.entries(person));
// 出力: [['name', 'Alice'], ['age', 25], ['country', 'Japan']]
```

このメソッドは、キーと値のペアを直接操作する際に、たとえばマップオブジェクトに変換するときなどに便利です。

## 使用場面と実践的なヒント

- `Object.values()`は、オブジェクトの値に基づく操作や計算を行う際に役立ちます。
- `Object.keys()`は、オブジェクトのプロパティを検査したり、プロパティの存在を確認したりするのに使用されます。
- `Object.entries()`は、オブジェクトのキーと値のペアを繰り返し処理する際に最適です。例えば、オブジェクトをマップや他のデータ構造に変換する場合などです。

## 関連記事

1. **MDN Web Docs** - [Object.values()](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Object/values)  
   このページでは`Object.values()`メソッドについて詳しく説明しており、使用例やメソッドの挙動についても触れられています。

2. **MDN Web Docs** - [Object.keys()](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)  
   `Object.keys()`メソッドに焦点を当てたこの記事では、メソッドの使用法としての詳細な説明と共に、実用的なコード例が提供されています。

3. **MDN Web Docs** - [Object.entries()](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Object/entries)  
   `Object.entries()`メソッドの詳細な解説が行われているこのページでは、メソッドの構文、使用例、および関連する情報が豊富に含まれています。
