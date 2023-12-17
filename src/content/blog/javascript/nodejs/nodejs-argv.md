---
author: Taro Gray
pubDatetime: 2023-12-17T23:18:00.00Z
title: Node.jsの`argv`で始めるCLIアプリケーション開発
postSlug: nodejs-argv
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - NodeJS
  - argv
description: Node.jsの`process.argv`は、コマンドライン引数を扱う際に非常に便利です。この記事では、`argv`を使ってCLIアプリケーションを作る方法を面白い例と共に解説します。
---

## Table of contents

## Node.jsの`argv`で始めるCLIアプリケーション開発

Node.jsの`process.argv`は、コマンドライン引数を扱う際に非常に便利です。この記事では、`argv`を使ってCLIアプリケーションを作る方法を面白い例と共に解説します。

## 1. `argv`の基本

`process.argv`は、コマンドラインから渡された引数の配列です。

```javascript
// app.js
process.argv.forEach((val, index) => {
  console.log(`${index}: ${val}`);
});

// コマンドラインから実行: node app.js arg1 arg2
// 出力:
// 0: path/to/node
// 1: path/to/app.js
// 2: arg1
// 3: arg2
```

## 2. 引数を使ったシンプルなCLIアプリ

引数を利用して、特定の操作を実行するCLIアプリを作成できます。

```javascript
// greet.js
const name = process.argv[2];

console.log(`Hello, ${name}!`);

// コマンドラインから実行: node greet.js Alice
// 出力: Hello, Alice!
```

## 3. より複雑なCLIアプリ

複数の引数を使った複雑なCLIアプリケーションも作成可能です。

```javascript
// calc.js
const [operation, num1, num2] = process.argv.slice(2);

const result =
  operation === "add" ? parseInt(num1) + parseInt(num2) : "Unknown operation";

console.log(`Result: ${result}`);

// コマンドラインから実行: node calc.js add 5 3
// 出力: Result: 8
```

## 4. 面白い例：宇宙船のコントロールCLI

面白い例として、宇宙船をコントロールするCLIアプリケーションを作ってみましょう。

```javascript
// spaceship.js
const [action, value] = process.argv.slice(2);

switch (action) {
  case "launch":
    console.log(`Launching spaceship at speed ${value} lightyears/hour!`);
    break;
  case "land":
    console.log(`Landing spaceship on planet ${value}!`);
    break;
  default:
    console.log("Unknown action");
}

// コマンドラインから実行: node spaceship.js launch 5
// 出力: Launching spaceship at speed 5 lightyears/hour!
```

この架空の例では、宇宙船の発射や着陸をコマンドラインからコントロールしています。

## 5. ハッカーとCLIアプリ

ハッカーもCLIアプリケーションを使って、システムの状態を確認したり操作したりすることがあります。

```javascript
// hack.js
const target = process.argv[2];

console.log(`Attempting to hack ${target}...`);

// コマンドラインから実行: node hack.js Mainframe
// 出力: Attempting to hack Mainframe...
```

この架空の例では、ハッカーがCLIを通じて特定のターゲットに対する攻撃を試みています。
Node.jsの`process.argv`を使うと、簡単にCLIアプリケーションを作成できます。この記事で紹介した面白い例を通じて、CLIアプリの開発の楽しさを味わっていただければ幸いです
