---
author: Taro Gray
pubDatetime: 2024-09-02T19:00:00.00Z
title: Javaのboxed()を使ってプリミティブ型をオブジェクト型に変換する
postSlug: java-using-boxed-method-in-stream
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Stream API
description: Javaの`boxed()`メソッドを使って、プリミティブ型のStreamをラッパークラスに変換する方法を解説します。IntStreamやDoubleStreamの処理をオブジェクト型に変換する利点と使用例も紹介します。
---

## Table of contents

## 1. `boxed()`とは？

`boxed()`は、Javaの`Stream` APIで提供されているメソッドの一つで、プリミティブ型のストリーム（`IntStream`, `LongStream`, `DoubleStream`など）をその対応するラッパークラス（`Integer`, `Long`, `Double`など）のストリームに変換するために使用されます。

### 例えば:

- `IntStream` を `Stream<Integer>` に変換
- `DoubleStream` を `Stream<Double>` に変換

`boxed()`メソッドは、プリミティブ型のストリームとオブジェクト型のストリームを区別するための重要な役割を持っています。プリミティブ型はメモリ効率のために軽量ですが、オブジェクト型のデータ処理が必要な場合には、`boxed()`を使って変換します。

## 2. 基本型とラッパークラス

Javaでは、基本型（プリミティブ型）として `int`, `long`, `double` などがありますが、これらには対応する**ラッパークラス**が存在します。

| 基本型   | ラッパークラス |
| -------- | -------------- |
| `int`    | `Integer`      |
| `long`   | `Long`         |
| `double` | `Double`       |

基本型は、数値や文字などのデータを軽量に扱うために使われ、メモリやパフォーマンスが最適化されています。一方、ラッパークラスは、基本型をオブジェクトとして扱えるようにするクラスです。ラッパークラスを使うと、基本型データをコレクション（`List`, `Set`, `Map`）に格納したり、関数に渡すことができます。

## 3. `boxed()`の使い方

`boxed()`は、プリミティブ型のストリームをオブジェクト型に変換するために使われます。ここでは、`IntStream`を例に挙げて、`boxed()`の使い方を見てみましょう。

### `boxed()`のコード例

```java
import java.util.stream.IntStream;
import java.util.List;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        // IntStreamをStream<Integer>に変換
        List<Integer> list = IntStream.range(1, 5)  // 1から4までのIntStream
                                      .boxed()      // Stream<Integer>に変換
                                      .collect(Collectors.toList()); // Listに収集

        System.out.println(list); // 出力: [1, 2, 3, 4]
    }
}
```

### 解説

- `IntStream.range(1, 5)` は、1から4までの整数を持つプリミティブ型の`IntStream`を生成します。
- `.boxed()` を呼び出すことで、`IntStream`を`Stream<Integer>`に変換しています。
- 最終的に、`collect(Collectors.toList())` を使用して、`Stream<Integer>` を `List<Integer>` に変換しています。

## 4. なぜ`boxed()`が必要か？

`boxed()`が必要となるのは、プリミティブ型のストリームを操作しているときに、オブジェクト型が必要な操作を行いたい場合です。`IntStream`, `DoubleStream` などのプリミティブ型ストリームは軽量で効率的ですが、オブジェクト型の操作をサポートしていないため、`boxed()`で変換が必要です。

### プリミティブ型とオブジェクト型の違い

- **プリミティブ型ストリーム (`IntStream`, `DoubleStream`など)**: 基本型でメモリ効率が高い。コレクションや`Collectors`の一部と直接連携できない。
- **オブジェクト型ストリーム (`Stream<Integer>`, `Stream<Double>`など)**: オブジェクトを扱うため、コレクションへの変換や特定の操作（`Collectors.toList()` など）が可能。

例えば、`IntStream`や`DoubleStream`は、`Collectors.toList()`や`Collectors.toSet()`のようなメソッドとは直接互換性がありません。これらのメソッドを使いたい場合、`boxed()`を使ってプリミティブ型をオブジェクト型に変換する必要があります。

### 別の例

```java
import java.util.stream.DoubleStream;
import java.util.Set;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        // DoubleStreamをStream<Double>に変換し、Setに収集
        Set<Double> set = DoubleStream.of(1.1, 2.2, 3.3)
                                      .boxed()  // Stream<Double>に変換
                                      .collect(Collectors.toSet()); // Setに収集

        System.out.println(set); // 出力: [1.1, 2.2, 3.3]
    }
}
```

この例では、`DoubleStream`を`boxed()`で`Stream<Double>`に変換し、`Set<Double>`に収集しています。

## 5. まとめ

Javaの`boxed()`メソッドは、プリミティブ型のストリームをラッパークラス（オブジェクト型）のストリームに変換するための便利なツールです。`boxed()`を使用することで、`Stream` APIの多くのメソッドと互換性を持たせたり、`List`, `Set` などのコレクションに変換できるようになります。

### ポイント:

- `boxed()`を使うと、プリミティブ型の`Stream`をオブジェクト型の`Stream`に変換できます。
- オブジェクト型の`Stream`は、`Collectors.toList()`や`Collectors.toSet()`などのメソッドと互換性があります。
- メモリ効率の高いプリミティブ型を扱いつつ、オブジェクト型の操作が必要な場合に`boxed()`は便利です。
