---
author: Taro Gray
pubDatetime: 2023-12-03T05:12:00.007Z
title:  Node.jsのジェネレータ：非同期以外の面白い使い方
postSlug: javascript-generator 
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Javascript
  - generator 
description: 
Node.jsのジェネレータは非同期プログラミングだけでなく、多様な用途に利用できる強力なツールです。この記事では、`Array`、`Map`、`Set`に関連するジェネレータの使い方を面白い例と共に紹介します。
---

## Table of contents

## Node.jsのジェネレータ：非同期以外の面白い使い方

Node.jsのジェネレータは非同期プログラミングだけでなく、多様な用途に利用できる強力なツールです。この記事では、`Array`、`Map`、`Set`に関連するジェネレータの使い方を面白い例と共に紹介します。

## 1. ジェネレータと配列

ジェネレータは、配列の要素を動的に生成する際に便利です。

```javascript
function* generateNumbers(limit) {
  for (let i = 0; i < limit; i++) {
    yield i;
  }
}

const numberGenerator = generateNumbers(5);
const numbersArray = Array.from(numberGenerator);
console.log(numbersArray); // [0, 1, 2, 3, 4]
```

## 2. ジェネレータとマップ

ジェネレータを使用して、キーと値のペアを持つマップを生成することができます。

```javascript
function* generateKeyValuePairs(pairs) {
  for (const pair of pairs) {
    yield pair;
  }
}

const mapGenerator = generateKeyValuePairs([
  ["key1", "value1"],
  ["key2", "value2"],
]);
const map = new Map(mapGenerator);
console.log(map); // Map { 'key1' => 'value1', 'key2' => 'value2' }
```

## 3. ジェネレータとセット

ジェネレータはセットの要素を生成するためにも使用できます。

```javascript
function* generateSetValues(values) {
  for (const value of values) {
    yield value;
  }
}

const setGenerator = generateSetValues([1, 2, 3, 4, 5]);
const set = new Set(setGenerator);
console.log(set); // Set { 1, 2, 3, 4, 5 }
```

## 4. 面白い例：ハッカーのパスワードジェネレータ

面白い例として、ハッカーが使用するかもしれないパスワードジェネレータを作ってみましょう。

```javascript
function* passwordGenerator(words) {
  for (const word of words) {
    for (let i = 0; i < 1000; i++) {
      yield `${word}${i}`;
    }
  }
}

const hackerPasswords = passwordGenerator(["hack", "secret"]);
for (let i = 0; i < 5; i++) {
  console.log(hackerPasswords.next().value);
}
// hack0, hack1, hack2, hack3, hack4...
```

この架空の例では、ハッカーが基本的な単語に数値を組み合わせたパスワードを生成しています。

## まとめ

ジェネレータは、Node.jsでのデータ構造の操作をより柔軟かつ強力にするための素晴らしいツールです。面白い例を通じて、ジェネレータの様々な使用方法を楽しく学んでいただければ幸いです。ハッピーハッキング！
