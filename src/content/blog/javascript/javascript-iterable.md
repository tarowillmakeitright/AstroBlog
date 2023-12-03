---
author: Taro Gray
pubDatetime: 2023-12-03T05:19:00.007Z
title: Node.jsのイテレータとイテラブル：楽しく探索するデータの旅
postSlug: javascript-iterable
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Javascript
  - iterable
description: Node.jsでのイテレータとイテラブルは、データ構造を順序立ててアクセスするための強力な概念です。この記事では、イテレータとイテラブルの基本から、面白いコード例を通じてその使用方法を探ります。
---

## Table of contents

## Node.jsのイテレータとイテラブル：楽しく探索するデータの旅

Node.jsでのイテレータとイテラブルは、データ構造を順序立ててアクセスするための強力な概念です。この記事では、イテレータとイテラブルの基本から、面白いコード例を通じてその使用方法を探ります。

## 1. イテレータとは？

イテレータは、コレクションの要素に順番にアクセスするためのオブジェクトです。`next()`メソッドを呼び出すことで、`{ value, done }`の形式で要素を取得できます。

```javascript
function makeRangeIterator(start = 0, end = Infinity, step = 1) {
  let nextIndex = start;
  let iterationCount = 0;

  const rangeIterator = {
    next: function () {
      let result;
      if (nextIndex < end) {
        result = { value: nextIndex, done: false };
        nextIndex += step;
        iterationCount++;
        return result;
      }
      return { value: iterationCount, done: true };
    },
  };
  return rangeIterator;
}

const it = makeRangeIterator(1, 10, 2);

let result = it.next();
while (!result.done) {
  console.log(result.value); // 1, 3, 5, 7, 9
  result = it.next();
}
console.log("Iterated over sequence of size: ", result.value); // 5
```

## 2. イテラブルとは？

イテラブルは、そのオブジェクトがイテレータを持っており、`for...of`ループなどで反復可能であることを意味します。

```javascript
const iterable = {
  [Symbol.iterator]() {
    return makeRangeIterator(1, 5);
  },
};

for (const value of iterable) {
  console.log(value); // 1, 2, 3, 4
}
```

## 3. 面白い例：宇宙探索イテラブル

面白い例として、宇宙探索を行うイテラブルを考えてみましょう。

```javascript
const spaceAdventure = {
  planets: ["Mercury", "Venus", "Earth", "Mars"],
  [Symbol.iterator]() {
    let index = 0;
    return {
      next: () => {
        const value = this.planets[index];
        const done = index >= this.planets.length;
        index++;
        return { value, done };
      },
    };
  },
};

for (const planet of spaceAdventure) {
  console.log(`Exploring: ${planet}`);
}
```

この例では、イテラブルを通じて宇宙の惑星を順番に探索しています。

## 4. ハッカーとイテレータ

ハッカーはイテレータを利用して、データセットを効率的に探索することがあります。

```javascript
const hackableSystems = {
  systems: ["Server", "Database", "Network"],
  [Symbol.iterator]() {
    let index = 0;
    return {
      next: () => {
        const value = this.systems[index];
        const done = index >= this.systems.length;
        index++;
        return { value, done };
      },
    };
  },
};

for (const system of hackableSystems) {
  console.log(`Hacking: ${system}`);
}
```

この架空の例では、ハッカーがシステムを順にハックしていく様子をイテラブルで表現しています。

## まとめ

イテレータとイテラブルは、データの反復処理をシンプルかつ効率的に行うための強力なツールです。面白い例を通じて、これらの概念を楽しく学んでいただければ幸いです。ハッピーハッキング！
