---
author: Taro Gray
pubDatetime: 2023-11-16T11:36:00.00Z
title: 【Javascript DOM編】Nodeオブジェクトについて
postSlug: dom-node-object
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Javascript
  - DOM
  - Node
  - オブジェクト
description: JavaScriptのDOMにおける`Node`オブジェクトは、DOMツリーの基本的な構成要素です。`Node`オブジェクトには多くのプロパティがありますが、ここでは主要なものを挙げ、それぞれについて簡単な説明とコード例を提供します。
---

## Table of contents

JavaScriptのDOMにおける`Node`オブジェクトは、DOMツリーの基本的な構成要素です。`Node`オブジェクトには多くのプロパティがありますが、ここでは主要なものを挙げ、それぞれについて簡単な説明とコード例を提供します。

## 1. nodeName

- **概要**: `nodeName`は、ノードの名前を表します。要素ノードの場合はタグ名、テキストノードの場合は`#text`、ドキュメントノードの場合は`#document`などが返されます。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  console.log(element.nodeName); // 要素のタグ名を出力
  ```

## 2. nodeType

- **概要**: `nodeType`は、ノードのタイプを表す数値を返します（例：1 = Element, 3 = Text）。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  console.log(element.nodeType); // ノードタイプを出力
  ```

## 3. parentNode

- **概要**: `parentNode`は、ノードの親ノードを返します。親ノードがない場合は`null`を返します。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  console.log(element.parentNode); // 親ノードを出力
  ```

## 4. childNodes

- **概要**: すでに述べたように、`childNodes`はノードの子ノードのリストを返します。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  console.log(element.childNodes); // 子ノードのリストを出力
  ```

## 5. firstChild / lastChild

- **概要**: `firstChild`は最初の子ノードを、`lastChild`は最後の子ノードを返します。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  console.log(element.firstChild); // 最初の子ノードを出力
  console.log(element.lastChild); // 最後の子ノードを出力
  ```

## 6. previousSibling / nextSibling

- **概要**: `previousSibling`は、現在のノードの前にある兄弟ノードを返します。`nextSibling`は後にある兄弟ノードを返します。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  console.log(element.previousSibling); // 前の兄弟ノードを出力
  console.log(element.nextSibling); // 次の兄弟ノードを出力
  ```

これらのプロパティは、DOMツリーの構造やノード間の関係を理解し操作する上で非常に重要です。また、これらのプロパティを活用することで、Webページ上の要素を動的に変更したり、ユーザーのインタラクションに応じてコンテンツを更新するなどの操作が可能になります。
