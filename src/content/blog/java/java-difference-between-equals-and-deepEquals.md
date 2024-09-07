---
author: Taro Gray
pubDatetime: 2024-09-02T20:00:00.00Z
title: Javaのequals()とdeepEquals()の違いとは?
postSlug: difference-between-equals-and-deepEquals-in-java
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - equals
  - deepEquals
description: Javaにおける`equals()`と`deepEquals()`の違いについて解説。基本的なオブジェクトの比較方法や、ネストされた配列の比較など、それぞれのメソッドの使いどころを紹介します。
---

## Table of contents

## 1. `equals()`とは？

`equals()` は、Javaでオブジェクトの「値」が等しいかどうかを比較するために使用されるメソッドです。Javaのすべてのオブジェクトは`Object`クラスを継承しており、`equals()`メソッドも`Object`クラスから提供されます。

### `equals()`の特性

- 基本的には「オブジェクトの参照」を比較します。
- クラスによっては、`equals()` メソッドがオーバーライドされており、参照ではなくオブジェクトの「値」が同じかどうかを比較します（例: `String`や`Integer`クラス）。
- 配列の場合、`equals()`は配列の要素を比較するのではなく、配列の「参照」を比較するため、異なるオブジェクトであれば内容が同じでも`false`を返します。

### 例: `equals()`の使い方

```java
String s1 = new String("Hello");
String s2 = new String("Hello");

System.out.println(s1.equals(s2)); // true (値が同じ)

int[] arr1 = {1, 2, 3};
int[] arr2 = {1, 2, 3};

System.out.println(arr1.equals(arr2)); // false (参照が異なるため)
```

この例では、`String`オブジェクトは`equals()`をオーバーライドしているため、文字列の「値」を比較して`true`を返します。一方で、配列は異なる参照であるため、内容が同じでも`false`を返します。

## 2. `deepEquals()`とは？

`deepEquals()` は、Javaの`Arrays`クラスで提供されているメソッドで、配列やネストされたオブジェクト（例えば、配列の中に配列が含まれる場合）を「深いレベル」で比較するために使用されます。

### `deepEquals()`の特性

- 配列やネストされたオブジェクトの各要素を再帰的に比較します。
- もし配列の要素が配列であっても、各要素の中身まで比較を行い、内容が同じであれば`true`を返します。
- 基本型やオブジェクト型に対しても再帰的に比較を行います。

### 例: `deepEquals()` の使い方

```java
import java.util.Arrays;

int[] arr1 = {1, 2, 3};
int[] arr2 = {1, 2, 3};

System.out.println(Arrays.deepEquals(arr1, arr2)); // true (要素が同じ)

Object[] obj1 = {new int[]{1, 2, 3}, new int[]{4, 5, 6}};
Object[] obj2 = {new int[]{1, 2, 3}, new int[]{4, 5, 6}};

System.out.println(Arrays.deepEquals(obj1, obj2)); // true (ネストされた配列も比較)
```

この例では、`Arrays.deepEquals()`を使って配列やネストされた配列を比較し、内容が同じであれば`true`を返しています。

## 3. `equals()` と `deepEquals()` の違い

| 比較項目         | `equals()`                                              | `deepEquals()`                                       |
| ---------------- | ------------------------------------------------------- | ---------------------------------------------------- |
| 使用場所         | `Object` クラスに存在し、すべてのオブジェクトで使用可能 | `Arrays` クラスで提供されており、配列の比較に特化    |
| 比較の対象       | オブジェクトの参照または、オーバーライドされた比較方法  | 配列やネストされたオブジェクトの全要素を再帰的に比較 |
| 配列の扱い       | 配列の参照を比較（同一オブジェクトかどうか）            | 配列の中身を比較（要素が同じかどうか）               |
| ネストされた配列 | ネストされた配列の参照のみを比較                        | ネストされた配列の中の要素を再帰的に比較             |
| 結果             | オブジェクトが同じかどうか（通常は参照を比較）          | 配列の内容が同じかどうか（深い比較が行われる）       |

### 例: 配列を比較する場合

`equals()` は参照の比較のみを行うため、異なる配列オブジェクトではたとえ内容が同じでも `false` になります。一方、`deepEquals()` を使えば配列の要素を再帰的に比較するため、内容が同じであれば `true` を返します。

## 4. まとめ

### `equals()`

- **参照**を比較するため、基本的には同じオブジェクトであるかを判定します。
- ただし、クラスによってはオーバーライドされており、`String`や`Integer`などのクラスでは「値」を比較します。
- 配列の場合、要素ではなく参照を比較するため、同じ内容の異なる配列は`false`を返します。

### `deepEquals()`

- 配列やネストされたオブジェクトの「要素」を再帰的に比較します。
- 配列の要素が同じ場合、異なるオブジェクトでも `true` を返します。
- ネストされたデータ構造を扱う場合に便利で、特に複雑なオブジェクトの比較には有効です。

`equals()` と `deepEquals()` は、オブジェクトの比較方法が異なるため、使い分けが重要です。特に配列やネストされたデータ構造を扱う場合は、`deepEquals()`を使用することで正確な比較が行えます。
