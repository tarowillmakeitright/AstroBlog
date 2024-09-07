---
author: Taro Gray
pubDatetime: 2024-09-07T15:27:00.00Z
title: JavaのComparatorを使ったカスタムソートと便利なメソッド
postSlug: java-custom-sorting-comparator
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Comparator
description: JavaのComparatorを使って、オブジェクトを価格や名前でカスタムソートする方法を解説。さらに、Comparatorの便利なメソッドも紹介します。
---

## Table of contents

## 1. `Comparator`とは？

Javaの`Comparator`インターフェースは、カスタムのオブジェクトを特定の基準に基づいて比較・ソートするために使われます。`Comparator`を使うことで、リストや配列内のオブジェクトを価格、名前、日付など任意の条件でソートできます。

デフォルトでは、Javaのコレクション（例えば、`List`や`Array`）は自然順序（`Comparable`インターフェースを実装したオブジェクトによる順序）でソートされますが、`Comparator`を使うと、カスタムのソートロジックを提供できます。

### `Comparator`のメソッド

- **`compare(T o1, T o2)`**: 2つのオブジェクトを比較します。このメソッドを実装することで、オブジェクトの並び順を定義します。
  - 正の数: `o1`が`o2`より大きい
  - 0: `o1`と`o2`が等しい
  - 負の数: `o1`が`o2`より小さい

## 2. `PriceComparator`と`NameComparator`の実装

### `PriceComparator`の実装

`PriceComparator`は、商品の価格に基づいてオブジェクトを比較するためのクラスです。昇順または降順でソートすることができます。

```java
import java.util.Comparator;

class Item {
    private String name;
    private double price;

    public Item(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public String getName() {
        return name;
    }

    public double getPrice() {
        return price;
    }

    @Override
    public String toString() {
        return name + ": " + price;
    }
}

// PriceComparatorを作成
class PriceComparator implements Comparator<Item> {
    @Override
    public int compare(Item item1, Item item2) {
        return Double.compare(item1.getPrice(), item2.getPrice());
    }
}
```

### `NameComparator`の実装

`NameComparator`は、商品の名前に基づいてアルファベット順にソートします。

```java
import java.util.Comparator;

class NameComparator implements Comparator<Item> {
    @Override
    public int compare(Item item1, Item item2) {
        return item1.getName().compareTo(item2.getName());
    }
}
```

## 3. `Comparator`を使ったソート例

これらのコンパレータを使って、アイテムリストを価格や名前でソートする例を見てみましょう。

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Item> itemList = new ArrayList<>();
        itemList.add(new Item("Apple", 1.50));
        itemList.add(new Item("Banana", 0.99));
        itemList.add(new Item("Cherry", 2.50));

        // 価格で昇順にソート
        Collections.sort(itemList, new PriceComparator());
        System.out.println("Price sorted list:");
        for (Item item : itemList) {
            System.out.println(item);
        }

        // 名前でアルファベット順にソート
        Collections.sort(itemList, new NameComparator());
        System.out.println("Name sorted list:");
        for (Item item : itemList) {
            System.out.println(item);
        }
    }
}
```

### 出力例:

```
Price sorted list:
Banana: 0.99
Apple: 1.5
Cherry: 2.5

Name sorted list:
Apple: 1.5
Banana: 0.99
Cherry: 2.5
```

## 4. 他の便利な`Comparator`メソッド

`Comparator`は、カスタムの比較ロジックを簡単に記述できるよう、いくつかの便利な静的メソッドを提供しています。ここでは、その中でもよく使われるものを紹介します。

### `reversed()`

`Comparator`を反転して、昇順から降順、またはその逆にするメソッドです。`Comparator`の結果を簡単に逆にしたい場合に使います。

```java
// 価格で降順にソート
Collections.sort(itemList, new PriceComparator().reversed());
```

### `thenComparing()`

`thenComparing`は、1つ目の比較が等しい場合に、2つ目の条件でさらに比較を行うためのメソッドです。複数の条件でソートを行いたいときに使います。

```java
// まず価格で昇順、同じ価格の場合は名前でソート
Collections.sort(itemList, new PriceComparator().thenComparing(new NameComparator()));
```

### `comparing()`

`Comparator.comparing()`は、ラムダ式を使って比較の基準を指定できるメソッドです。これにより、`Comparator`の生成が非常にシンプルになります。

```java
// 名前でソート（ラムダ式を使用）
Collections.sort(itemList, Comparator.comparing(Item::getName));

// 価格でソート
Collections.sort(itemList, Comparator.comparing(Item::getPrice));
```

### `nullsFirst()` と `nullsLast()`

`null` 値を含むデータセットをソートする場合、`null` を優先する（`nullsFirst`）、または最後に回す（`nullsLast`）という操作が可能です。

```java
// 名前がnullのアイテムを優先してソート
Collections.sort(itemList, Comparator.comparing(Item::getName, Comparator.nullsFirst(String::compareTo)));
```

## 5. まとめ

Javaの`Comparator`を使うことで、オブジェクトのソートを簡単にカスタマイズでき、価格や名前など特定の属性に基づいた柔軟なソートが可能になります。`Comparator`は、リストやセットをソートする際に非常に便利で、`thenComparing`や`reversed`などのメソッドを使うことで、より複雑な条件に基づいたソートも簡単に実装できます。

- **`PriceComparator`**: 商品の価格に基づいて昇順または降順でソート
- **`NameComparator`**: 名前に基づいてアルファベット順にソート
- **便利な`Comparator`メソッド**: `reversed()`, `thenComparing()`, `comparing()`, `nullsFirst()` など
