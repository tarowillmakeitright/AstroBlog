---
author: Taro Gray
pubDatetime: 2024-09-07T15:51:00.00Z
title: Java Streamの中間操作を徹底解説
postSlug: java-stream-intermediate-operations
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Stream API
description: JavaのStream APIにおける中間操作について詳しく解説します。中間操作は、データのフィルタリングやマッピングなど、Stream内でのデータ処理において重要な役割を果たします。
---

## Table of contetns

## 1. `Stream` APIの中間操作とは？

`Stream`の中間操作（Intermediate Operations）は、`Stream`内の要素をフィルタリングしたり、変換したり、並べ替えたりするために使用される操作です。中間操作は、`Stream`のデータを新しい形に変換し、最終的な結果（終端操作）に渡す準備をします。

中間操作は、**遅延評価（Lazy Evaluation）**されます。これは、`Stream`に中間操作をチェーンしただけでは何も実行されず、終端操作（`collect`, `forEach` など）によって初めて実行されるという意味です。

## 2. 中間操作の特徴

中間操作にはいくつかの特徴があります。

- **ステートレス操作とステートフル操作**: 中間操作には、過去の要素に依存しない「ステートレス操作」と、順序や要素全体に依存する「ステートフル操作」があります。例えば、`filter` はステートレスで、`sorted` はステートフルです。
- **遅延評価**: 中間操作は終端操作が実行されるまで評価されません。このため、無駄な処理が発生せず、効率的にデータを処理できます。

- **パイプライン構築**: 中間操作は `Stream` を返すため、複数の中間操作をチェーンして実行することができます。これにより、データ操作の流れをわかりやすく記述できます。

## 3. 代表的な中間操作

ここでは、よく使われる`Stream`の中間操作について解説します。

### 1. `filter()`

`filter` は、指定された条件に一致する要素のみを含む新しい`Stream`を生成します。

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
List<Integer> evenNumbers = numbers.stream()
                                   .filter(n -> n % 2 == 0) // 偶数をフィルタリング
                                   .collect(Collectors.toList());

System.out.println(evenNumbers); // 出力: [2, 4, 6, 8, 10]
```

### 2. `map()`

`map` は、`Stream`の各要素に対して関数を適用し、新しい要素に変換します。これは、データを別の形式に変換する場合に使われます。

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
List<String> upperCaseNames = names.stream()
                                   .map(String::toUpperCase) // すべての名前を大文字に変換
                                   .collect(Collectors.toList());

System.out.println(upperCaseNames); // 出力: [ALICE, BOB, CHARLIE]
```

### 3. `sorted()`

`sorted` は、`Stream`の要素を自然順序や指定した`Comparator`に従ってソートします。

```java
List<Integer> numbers = Arrays.asList(5, 2, 9, 1, 7);
List<Integer> sortedNumbers = numbers.stream()
                                     .sorted() // 自然順序でソート
                                     .collect(Collectors.toList());

System.out.println(sortedNumbers); // 出力: [1, 2, 5, 7, 9]
```

### 4. `distinct()`

`distinct` は、重複を取り除いてユニークな要素だけを含む`Stream`を生成します。

```java
List<String> names = Arrays.asList("Alice", "Bob", "Alice", "Charlie", "Bob");
List<String> uniqueNames = names.stream()
                                .distinct() // 重複を除去
                                .collect(Collectors.toList());

System.out.println(uniqueNames); // 出力: [Alice, Bob, Charlie]
```

### 5. `limit()`と`skip()`

- **`limit(n)`**: `Stream`の最初の`n`個の要素を取得します。
- **`skip(n)`**: `Stream`の最初の`n`個の要素をスキップし、残りの要素を取得します。

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);
List<Integer> limitedNumbers = numbers.stream()
                                      .limit(5) // 最初の5個の要素
                                      .collect(Collectors.toList());

System.out.println(limitedNumbers); // 出力: [1, 2, 3, 4, 5]

List<Integer> skippedNumbers = numbers.stream()
                                      .skip(5) // 最初の5個の要素をスキップ
                                      .collect(Collectors.toList());

System.out.println(skippedNumbers); // 出力: [6, 7, 8, 9, 10]
```

## 4. `Stream`の中間操作を使った実例

中間操作を組み合わせて、データをフィルタリング、マッピング、ソートするパイプラインを構築できます。

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class StreamIntermediateExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "Dave", "Eve", "Frank");

        // 名前をフィルタリング、マッピング、ソート
        List<String> result = names.stream()
                                   .filter(name -> name.length() > 3) // 名前の長さが3文字以上
                                   .map(String::toUpperCase)          // 大文字に変換
                                   .sorted()                          // ソート
                                   .collect(Collectors.toList());

        System.out.println(result); // 出力: [ALICE, CHARLIE, DAVE, FRANK]
    }
}
```

この例では、名前のリストに対して以下の処理を行っています。

1. **フィルタリング**: 名前の長さが3文字以上のものだけを選択
2. **マッピング**: すべての名前を大文字に変換
3. **ソート**: 名前をアルファベット順にソート

これにより、効率的にデータを操作することができます。

## 5. まとめ

Javaの`Stream` APIにおける中間操作は、データを操作・変換する強力な手段です。`filter`, `map`, `sorted`, `distinct` などの中間操作をチェーンして使うことで、複雑なデータ処理を簡潔に記述できるのが特徴です。また、遅延評価により、効率的なデータ処理が可能になります。

中間操作を理解し、うまく活用することで、より柔軟でパフォーマンスの高いJavaプログラムを作成することができます。`Stream`の強力な機能を活用し、コレクション操作をさらに効率化してみましょう！
