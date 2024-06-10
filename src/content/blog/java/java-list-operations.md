---
author: Taro Gray
pubDatetime: 2024-05-13T12:00:00.00Z
title: Java リスト操作の基本
postSlug: java-list-operations
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Programming
  - List Operations
description: Java でのリスト操作は日常的なプログラミング作業で非常によく使用されます。この記事では、Java の List インターフェースを使った基本的な操作方法を紹介します。
---

## Table of Contents

## Java リストの作成と初期化

Java でリストを作成する基本的な方法は `ArrayList` クラスを使用することです。以下のコードは、文字列のリストを作成して初期化する方法を示しています。

```java
import java.util.ArrayList;
import java.util.List;

List<String> list1 = new ArrayList<>();
list1.add("A");
list1.add("B");
list1.add("C");
```

このリスト `list1` には、"A"、"B"、"C" という三つの文字列が含まれています。リストに要素を追加するには `add` メソッドを使用します。

## リストの要素の取得

リストから特定の要素を取得するには `get` メソッドを使用します。以下の例では、リスト `list1` のインデックス0にある要素を取得しています。

```java
String element0 = list1.get(0);
```

このメソッドは指定したインデックスにある要素を返します。インデックスがリストのサイズ外の場合は `IndexOutOfBoundsException` をスローします。

## リストのサイズの取得

リストのサイズ、つまりリストに含まれる要素の数を知りたい場合は `size` メソッドを使用します。

```java
Integer listsize = list1.size();
```

この値はリストに現在格納されている要素の数を返します。この情報は、for ループでリストを反復処理する際に特に役立ちます。

## リストの部分リストの取得

リストの特定の範囲の要素のみを含む新しいリストを作成したい場合は `subList` メソッドを使用します。このメソッドは、指定された開始インデックスと終了インデックスの間の要素を含む新しいリストを返します。

```java
List<String> sublist1 = list1.subList(1, 3);
```

この例では、`list1` のインデックス1からインデックス2までの要素（インデックス3は含まれない）を新しいリストとして取得しています。

## 要素のインデックスの検索

リスト内で特定の要素の位置を知りたい場合は `indexOf` メソッドを使用します。このメソッドは、指定された要素がリスト内で最初に出現する位置のインデックスを返します。

```java
Integer index1 = list1.indexOf("C");
```

このコードは、リスト `list1` 内の文字列 "C" のインデックスを返します。もし指定した要素がリストに存在しない場合、このメソッドは `-1` を返します。

以上の方法を利用することで、
