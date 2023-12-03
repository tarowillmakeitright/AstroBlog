---
author: Taro Gray
pubDatetime: 2023-12-03T05:50:00.00Z
title: CommonJSモジュール：JavaScriptの楽しさを探索
postSlug: javascript-common-js
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Javascript
  - Common-JS
description: JavaScriptのCommonJSモジュールシステムは、モジュールの読み込みやエクスポートを容易にします。この記事では、CommonJSの基本的な要素を面白く学びましょう！
---

## Table of contents

## CommonJSモジュール：JavaScriptの楽しさを探索

JavaScriptのCommonJSモジュールシステムは、モジュールの読み込みやエクスポートを容易にします。この記事では、CommonJSの基本的な要素を面白く学びましょう！

## 1. 'require()'と'module.exports'

CommonJSでは、`require()`関数を使用して他のファイルのモジュールを読み込み、`module.exports`を使用してモジュールをエクスポートします。

```javascript
// math.js
function add(a, b) {
  return a + b;
}

module.exports = add;

// app.js
const add = require("./math");
console.log(add(5, 3)); // 8
```

## 2. '**filename'と'**dirname'

`__filename`は現在のモジュールのファイル名を、`__dirname`はディレクトリパスを提供します。

```javascript
console.log(__filename); // /path/to/current/module.js
console.log(__dirname); // /path/to/current
```

## 3. JSONの読み込み

CommonJSでは、JSONファイルも簡単に読み込むことができます。

```javascript
const config = require("./config.json");
console.log(config); // JSONオブジェクト
```

## 4. Strictモード

Strictモードを使用すると、より厳格なエラーチェックが行われます。

```javascript
"use strict";

x = 3.14; // エラー: xは定義されていません
```

## 5. 面白い例：宇宙ハッカーのモジュール

面白い例として、宇宙ハッカーのモジュールを考えてみましょう！

```javascript
// spaceHacker.js
module.exports = {
  hack() {
    console.log("Hacking the universe!");
  },
};

// app.js
const spaceHacker = require("./spaceHacker");
spaceHacker.hack(); // Hacking the universe!
```

この例では、宇宙ハッカーが宇宙をハックする機能を提供するモジュールを作成しています。

## 6. ハッカーとCommonJS

ハッカーはCommonJSを利用して、コードの再利用性を高めたり、依存関係を管理したりします。モジュール化されたコードは、より読みやすく、保守しやすいです。
CommonJSは、JavaScriptの構造を整理し、モジュールの取り扱いを簡単にします。面白い例を通じて、CommonJSの力を発見し、楽しんで学んでいただければと思います。ハッピーハッキング！
