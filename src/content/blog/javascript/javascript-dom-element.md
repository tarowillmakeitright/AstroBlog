---
author: Taro Gray
pubDatetime: 2023-11-16T11:38:00.00Z
title: 【Javascript DOM編】Elementについて
postSlug: javascript-dom-element
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Javascript
  - DOM
  - Element
  - オブジェクト
description: JavaScriptのDOMにおける`Element`オブジェクトは、HTMLやXMLドキュメント内の要素を表します。`Element`は`Node`オブジェクトを継承しているため、`Node`のプロパティとメソッドをすべて持っていますが、さらに特有の機能も提供します。以下は`Element`オブジェクトの主要なプロパティとメソッドに関する説明と例です。
---

## Table of contents

JavaScriptのDOMにおける`Element`オブジェクトは、HTMLやXMLドキュメント内の要素を表します。`Element`は`Node`オブジェクトを継承しているため、`Node`のプロパティとメソッドをすべて持っていますが、さらに特有の機能も提供します。以下は`Element`オブジェクトの主要なプロパティとメソッドに関する説明と例です。

## プロパティ

### 1. tagName

- **概要**: `tagName`は、要素のタグ名を大文字（HTMLの場合）または小文字（XMLの場合）で返します。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  console.log(element.tagName); // 例: 'DIV' が返される場合がある
  ```

## 2. id

- **概要**: `id`プロパティは、要素のID属性の値を取得または設定します。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  console.log(element.id); // 要素のIDを出力
  ```

## 3. className

- **概要**: `className`は、要素のclass属性の値を取得または設定します。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  console.log(element.className); // 要素のクラス名を出力
  ```

## 4. innerHTML / outerHTML

- **概要**: `innerHTML`は要素内のHTMLまたはXMLを取得または設定します。`outerHTML`は、要素自体を含むHTMLを取得または設定します。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  console.log(element.innerHTML); // 要素内のHTMLを出力
  console.log(element.outerHTML); // 要素を含むHTMLを出力
  ```

## メソッド

## 1. getAttribute / setAttribute

- **概要**: `getAttribute`は、要素の指定された属性の値を返します。`setAttribute`は、指定された属性に値を設定します。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  console.log(element.getAttribute("data-custom")); // カスタム属性の値を出力
  element.setAttribute("data-custom", "newValue"); // カスタム属性の値を設定
  ```

## 2. querySelector / querySelectorAll

- **概要**: `querySelector`は、指定されたセレクターにマッチする最初の子孫要素を返します。`querySelectorAll`は、マッチするすべての子孫要素を返します。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  let child = element.querySelector(".child-class"); // 最初の子孫要素を取得
  let children = element.querySelectorAll(".child-class"); // すべての子孫要素を取得
  ```

## 3. addEventListener / removeEventListener

- **概要**: イベントリスナーを追加または削除します。これにより、特定のイベントが発生した際の動作を定義できます。
- **例**:
  ```javascript
  let element = document.getElementById("myElement");
  element.addEventListener("click", function () {
    console.log("Element clicked!");
  });
  // イベントリスナーを削除する場合
  element.removeEventListener("click", functionName);
  ```

これらのプロパティとメソッドを使用することで、Webページの要素に対して様々な操作を行うことができ、動的なウェブアプリケーションを作成する際に非常に重要な役割を果たします。
