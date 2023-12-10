---
author: Taro Gray
pubDatetime: 2023-12-10T23:39:00.00Z
title: Node.jsのEventEmitter：イベント駆動プログラミングの楽しみ
postSlug: nodejs-eventEmitter-on-once-off-emit
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - NodeJS
  - EventEmitter
description: Node.jsのEventEmitterは、イベント駆動プログラミングを実現する強力なツールです。この記事では、`on`, `once`, `off`, `emit`メソッドを使った面白い例を通じて、EventEmitterの使い方を解説します。
---

## Table of contents

## Node.jsのEventEmitter：イベント駆動プログラミングの楽しみ

Node.jsのEventEmitterは、イベント駆動プログラミングを実現する強力なツールです。この記事では、`on`, `once`, `off`, `emit`メソッドを使った面白い例を通じて、EventEmitterの使い方を解説します。

## 1. EventEmitterの基本

EventEmitterは、イベントの発生をリッスンし、それに応じて関数を実行することができます。

```javascript
const EventEmitter = require("events");
const myEmitter = new EventEmitter();

myEmitter.on("event", () => {
  console.log("An event occurred!");
});

myEmitter.emit("event");
```

## 2. `once`メソッド

`once`メソッドは、イベントが一度だけ発生したときにリスナーを実行します。

```javascript
myEmitter.once("firstEvent", () => {
  console.log("First event only!");
});

myEmitter.emit("firstEvent");
myEmitter.emit("firstEvent"); // このイベントは無視される
```

## 3. `off`メソッド

`off`メソッドは、イベントリスナーを削除します。

```javascript
const callback = () => console.log("Event occurred!");
myEmitter.on("event", callback);

myEmitter.emit("event");
myEmitter.off("event", callback);
myEmitter.emit("event"); // イベントは無視される
```

## 4. `emit`メソッド

`emit`メソッドは、指定したイベントを発火させ、リスナーを呼び出します。

```javascript
myEmitter.emit("event", "arg1", "arg2");
```

## 5. 面白い例：宇宙船のイベントシステム

面白い例として、宇宙船のイベントシステムをEventEmitterで作ってみましょう。

```javascript
const spaceshipEmitter = new EventEmitter();

spaceshipEmitter.on("launch", () => {
  console.log("Spaceship launched!");
});

spaceshipEmitter.once("land", () => {
  console.log("Spaceship landed on Mars!");
});

spaceshipEmitter.emit("launch");
spaceshipEmitter.emit("land");
spaceshipEmitter.emit("land"); // このイベントは無視される
```

この架空の例では、宇宙船の発射と着陸イベントをEventEmitterで管理しています。

## 6. ハッカーとEventEmitter

ハッカーはEventEmitterを使用して、システムの特定のイベントをリッスンし、それに応じて行動することがあります。

```javascript
const systemEmitter = new EventEmitter();

systemEmitter.on("breach", message => {
  console.log(`Security breach detected: ${message}`);
});

systemEmitter.emit("breach", "Unauthorized access attempt");
```

この架空の例では、セキュリティ違反を検出するイベントリスナーを設定しています。
