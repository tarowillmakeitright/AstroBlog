---
author: Taro Gray
pubDatetime: 2024-09-07T14:00:00.00Z
title: Java Stream APIの基本と使い方
postSlug: java-stream-api-basics-and-usage
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Stream API
description: JavaのStream APIの使い方と利点を解説。Streamを使うことで、コレクション処理を簡潔かつ効率的に記述できます。
---

## Table of contents

## 1. `Stream` APIとは？

Javaの`Stream` APIは、コレクションや配列などのデータソースを処理するためのフレームワークです。Java 8で導入され、データ処理の効率を大幅に向上させるために使われます。

`Stream`は、データの連続した要素に対して、並列やシーケンシャルな操作を行うためのツールです。`Stream`は、一度だけ使用できるデータフローであり、操作の順序を指定することでデータの変換やフィルタリングなどが可能です。

## 2. `Stream`の基本操作

`Stream`は、主に次の3つのステップで構成されています。

1. **データソースからの`Stream`の生成**
2. **中間操作（Intermediate Operations）**: フィルタリング、マッピング、ソートなど
3. **終端操作（Terminal Operations）**: 結果を集約、収集、または出力する

### 基本的なメソッド

- **`filter`**: 条件に一致する要素を選択します。
- **`map`**: 各要素に対して変換を適用します。
- **`collect`**: 最終的な結果をリストやセットに収集します。

## 3. `Stream`を使った実用的なコード例

### 例1: リストから偶数だけを取り出す

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

        // 偶数だけをフィルタリング
        List<Integer> evenNumbers = numbers.stream()
                                           .filter(n -> n % 2 == 0)
                                           .collect(Collectors.toList());

        System.out.println("Even Numbers: " + evenNumbers);
    }
}
```

### 例2: リストの各要素を2倍に変換

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample {
    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // 各要素を2倍にする
        List<Integer> doubledNumbers = numbers.stream()
                                              .map(n -> n * 2)
                                              .collect(Collectors.toList());

        System.out.println("Doubled Numbers: " + doubledNumbers);
    }
}
```

### 例3: コレクションから重複を排除してソートする

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("John", "Alice", "Bob", "John", "Alice");

        // 重複を排除し、ソート
        List<String> uniqueSortedNames = names.stream()
                                              .distinct() // 重複を排除
                                              .sorted()   // ソート
                                              .collect(Collectors.toList());

        System.out.println("Unique Sorted Names: " + uniqueSortedNames);
    }
}
```

## 4. `Stream`の利点

`Stream`を使うと、コードがシンプルで読みやすくなります。また、`Stream`は遅延実行をサポートしており、データの処理が必要になるまで実行されないため、パフォーマンスが向上します。さらに、`parallelStream`を使えば並列処理が可能となり、大量のデータを効率的に処理することができます。

### 主な利点

- **シンプルなコード**: コレクション操作を簡潔に記述できる。
- **遅延評価**: 終端操作が呼び出されるまで中間操作は実行されない。
- **並列処理のサポート**: `parallelStream`を使うことで、並列処理によるパフォーマンス向上が可能。

## 5. まとめ

Javaの`Stream` APIは、コレクションやデータソースを効率的に処理するための強力なツールです。`filter`、`map`、`collect`といった操作を使うことで、複雑なデータ処理を簡潔に記述できます。さらに、`Stream` APIは並列処理をサポートしているため、大規模なデータセットを扱う際にも役立ちます。

`Stream`の活用は、コードの可読性を向上させ、効率的なデータ操作を可能にします。今後、さらに複雑な処理を行う場面でも、`Stream`の利用は非常に有益です。ぜひ、自分のプロジェクトで試してみてください！
