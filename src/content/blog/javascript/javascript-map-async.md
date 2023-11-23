---
author: Taro Gray
pubDatetime: 2023-10-31T11:45:54.547Z
title: Javascript Map 非同期処理についてわかりやすくまとめてみた
postSlug: post-3-javascript-map
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Javascript
  - マップ
  - map
  - 非同期処理
  - asynchronous
description: JavaScriptの`map`は、配列の各要素に対して関数を適用し、その結果からなる新しい配列を作成する高階関数です。これは関数型プログラミングの概念を活用しており、非常に便利です。
---

## Table of contents

## Map

JavaScriptの`map`は、配列の各要素に対して関数を適用し、その結果からなる新しい配列を作成する高階関数です。これは関数型プログラミングの概念を活用しており、非常に便利です。

### 基本的な使用法

以下は `map` 関数の基本的な使い方を示すコード例です。

```javascript
// 配列の各要素を2倍にする
const numbers = [1, 2, 3, 4];
const doubled = numbers.map(number => number * 2);
console.log(doubled); // [2, 4, 6, 8]
```

この例では、numbers という配列があり、map 関数を使用して各要素を2倍にしています。

###オブジェクトの配列での使用例

オブジェクトの配列で map を使用する例を見てみましょう。

```
// オブジェクトの配列があり、各オブジェクトの特定のプロパティで新しい配列を作る
const people = [
  { name: 'Alice', age: 25 },
  { name: 'Bob', age: 30 },
  { name: 'Carol', age: 35 }
];

// 'name' プロパティだけを抽出した新しい配列を作る
const names = people.map(person => person.name);
console.log(names); // ["Alice", "Bob", "Carol"]

```

### map 関数のシグネチャ

map 関数は以下のシグネチャを持っています。

```
arr.map(callback(currentValue[, index[, array]])[, thisArg])
```

- callback: 新しい配列の要素を生成するために元の配列の各要素に対して実行される関数。
- currentValue: 処理されている現在の要素。
- index（オプショナル）: 処理されている現在の要素のインデックス。
- array（オプショナル）: map が呼び出された配列。
- thisArg（オプショナル）: callback を実行する際に this として使用される値。

###注意点
map を使用する際の注意点は、callback 関数が必ず値を返す必要があることです。返された値は新しい配列の要素になります。
何も返さなければ、新しい配列の対応する要素は undefined になります。

## 非同期処理

非同期処理は、JavaScriptにおいて非常に重要な概念です。JavaScriptは単一スレッドで動作する言語ですが、WebブラウザやNode.jsなどの環境は非同期処理をサポートしています。これにより、長時間実行する操作（例えばネットワークリクエストやファイルI/O）がメインスレッドをブロックすることなく行えます。

### 非同期処理の基本

非同期処理は、特定のコードの実行完了を待たずに次の処理に進むことができるようにします。結果が準備でき次第、それを処理するためのコールバック関数を定義することが多いです。

たとえば、以下のコードでは`setTimeout`が非同期処理の一例です。`setTimeout`を使って、一定時間後にメッセージをログに出力しますが、その間に他のコードを実行することができます。

```javascript
console.log("処理を開始します。");

setTimeout(function () {
  console.log("指定された時間が経過しました。");
}, 2000);

console.log("setTimeoutは非同期で実行されます。");
```

このコードの実行結果は以下の通りです。

```
処理を開始します。
setTimeoutは非同期で実行されます。
指定された時間が経過しました。
```

`setTimeout`内の関数は2秒後に呼び出されますが、その間に他のログ出力が行われます。

## プロミス

非同期処理をより扱いやすくするために、プロミス（Promise）という機能が導入されました。プロミスは非同期操作が完了した後に結果またはエラーを返すオブジェクトです。プロミスを使うことで、非同期処理をより簡潔に、そして可読性高く書くことができます。

```javascript
let promise = new Promise(function (resolve, reject) {
  // 非同期処理
  setTimeout(function () {
    resolve("非同期処理の結果");
  }, 2000);
});

promise
  .then(function (value) {
    console.log(value); // '非同期処理の結果'
  })
  .catch(function (error) {
    console.log(error);
  });
```

## async/await

`async/await`はプロミスをさらに簡潔に書くための構文糖です。`async`を関数に付けることで、その関数はプロミスを返すようになります。`await`は、プロミスが解決されるのを待つために使用します。

```javascript
async function asyncFunction() {
  let promise = new Promise((resolve, reject) => {
    setTimeout(() => resolve("非同期処理完了！"), 2000);
  });

  let result = await promise; // プロミスが解決されるまで待つ
  console.log(result); // "非同期処理完了！"
}

asyncFunction();
```

この構文を使用すると、非同期コードが同期コードのように見えるため、読みやすくなります。

## エラー処理

非同期処理ではエラー処理も非常に重要です。プロミスでは`catch`を、`async/await`では`try/catch`構文を使用してエラーを捕捉します。

```javascript
async function asyncFunctionWithErrorHandling() {
  try {
    let promise = new Promise((resolve, reject) => {
      throw new Error('エラー発生！');
    });
    let result = await promise;
  } catch (error) {
    console.log
```
