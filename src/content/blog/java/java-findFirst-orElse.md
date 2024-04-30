---
author: Taro Gray
pubDatetime: 2024-01-28T22:16:00.00Z
title: Javaの探索術：findFirst()とorElse()
postSlug: java-findFirst-orElse
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
description: findFirst()`と`orElse()`は、Javaのストリームでデータを効率的に検索し、条件に一致する要素がない場合に備えるための強力なツールです。これらのメソッドを使いこなすことで、コードの柔軟性とロバストさを高めることができます。ぜひこれらのメソッドを活用して、あなたのコードに魔法をかけてください！
---

## Table of contents

こんにちは、Javaの世界の探索者たち！今日は、Stream APIの中でも特に便利な`findFirst()`と`orElse()`メソッドに焦点を当ててみましょう。これらのメソッドは、データの海から特定の要素を見つけ出し、もし見つからない場合には代替の値を提供する、まさに探索の達人のような存在です。それでは、中級者向けの具体例を交えて、この冒険を始めましょう。

## findFirst()とは？

`findFirst()`メソッドは、条件に一致するストリームの最初の要素を探し出すために使用されます。このメソッドは、`Optional`オブジェクトを返し、見つかった要素を格納します。

## orElse()とは？

`orElse()`メソッドは、`Optional`オブジェクトが値を含む場合はその値を返し、そうでない場合は指定された代替の値を返します。

## コード例：魔法のポーションを探す

想像してみてください、あなたは特定の効果を持つ魔法のポーションを探しています。しかし、もし探しているポーションが見つからない場合は、代わりに水を使うことにしましょう。

```java
import java.util.Arrays;
import java.util.List;
import java.util.Optional;

public class PotionSearch {

    public static void main(String[] args) {
        List<Potion> potions = Arrays.asList(
            new Potion("Invisibility"),
            new Potion("Healing"),
            new Potion("Strength")
        );

        Potion desiredPotion = potions.stream()
                                      .filter(potion -> "Flight".equals(potion.getName()))
                                      .findFirst()
                                      .orElse(new Potion("Water"));

        System.out.println("Found potion: " + desiredPotion.getName());
    }

    static class Potion {
        private String name;

        Potion(String name) {
            this.name = name;
        }

        String getName() {
            return name;
        }
    }
}
```

この例では、リスト`potions`から名前が"Flight"のポーションを探しています。`findFirst()`は最初に見つかった"Flight"ポーションを返しますが、もし存在しない場合、`orElse()`によって"Water"ポーションが代わりに返されます。

## リンクと参考文献

- [Oracle Java Documentation on Optional](https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html) - Javaの公式ドキュメントでの`Optional`に関する詳細。
- [Baeldung on Java Stream findFirst()](https://www.baeldung.com/java-stream-findfirst-vs-findany) - `findFirst()`と`findAny()`の比較に関する詳細な解説。
