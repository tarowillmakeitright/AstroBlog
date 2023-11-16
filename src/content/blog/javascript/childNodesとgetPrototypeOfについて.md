---
author: Taro Gray
pubDatetime: 2023-11-16T11:26:00.000Z
title: 【Javascript DOM編】childNodesとgetPrototypeOfについて
postSlug: childNodesとgetPrototypeOfについて
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Javascript
  - DOM
  - childNodes
  - getPrototypeOf
description: "JavaScriptのDOM（Document Object Model）に関して、`childNodes`と`getPrototypeOf`について説明します。"
---

## Table of contents

JavaScriptのDOM（Document Object Model）に関して、`childNodes`と`getPrototypeOf`について説明します。

## childNodes

- **概要**: `childNodes`は、あるノードの子ノードのコレクションを返します。これには、テキストノードやコメントノードなど、あらゆるタイプのノードが含まれます。
- **使用法**: `element.childNodes`の形で使用します。ここで`element`は任意のDOM要素です。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  let childNodes = element.childNodes;
  ```
  このコードは、`myElement`というIDを持つ要素の子ノードをすべて取得します。
- **注意点**: `childNodes`は生のノードリストを返すため、テキストやコメントノードも含まれることがあります。要素のみを取得したい場合は`children`プロパティを使用することが推奨されます。

## getPrototypeOf

- **概要**: `Object.getPrototypeOf`は、指定されたオブジェクトのプロトタイプ（つまり、内部プロパティ`[[Prototype]]`の値）を返します。これはJavaScriptのオブジェクト継承の基本的な機能の一つです。
- **使用法**: `Object.getPrototypeOf(obj)`の形で使用します。ここで`obj`は任意のオブジェクトです。
- **例**:
  ```javascript
  let proto = Object.getPrototypeOf(document.body);
  ```
  このコードは、`document.body`オブジェクトのプロトタイプを取得します。
- **注意点**: このメソッドはオブジェクトの内部プロトタイプチェーンを操作するため、特にプロトタイプ継承や動的なオブジェクト変更を行う際に重要です。ただし、プロトタイプチェーンの操作はパフォーマンスに影響を与える可能性があるため、慎重に使用する必要があります。

これらはJavaScriptでのDOM操作やオブジェクト指向プログラミングにおいて基本的な要素です。それぞれの使用法や挙動を理解することで、より複雑なDOM操作やオブジェクトの操作が可能になります。
