---
author: Taro Gray
pubDatetime: 2024-06-15T21:25:00.000Z
title: 2進数・10進数・16進数の変換と計算方法 Part 2
postSlug: basicInfo-numeral-systems-part-2
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - binary
  - decimal
  - hexadecimal
  - numeral-systems
description: 2進数、10進数、16進数の変換と基本的な計算方法についての解説
---

## Table of contents

## 2進数を10進数に変換する方法 Part 2

2進数を10進数に変換する手順は、各ビットにその位置の重みを掛けて足し合わせることです。以下に具体的な手順と例を示します。

### 手順

1. 各ビットに、そのビットが持つ位置の重み（2の累乗）を掛けます。
2. それらの値をすべて足し合わせます。

### 具体例

#### 問題

2進数 `1011` を10進数に変換します。

#### 解答

1. 各ビットに重みを掛けます。

   ```
   1 * 2^3 = 1 * 8 = 8
   0 * 2^2 = 0 * 4 = 0
   1 * 2^1 = 1 * 2 = 2
   1 * 2^0 = 1 * 1 = 1
   ```

2. それらの値を足し合わせます。
   ```
   8 + 0 + 2 + 1 = 11
   ```

したがって、2進数 `1011` は10進数で `11` です。

### さらに練習問題

#### 問題1

2進数 `1101` を10進数に変換してください。

#### 解答1

```
1 * 2^3 = 1 * 8 = 8
1 * 2^2 = 1 * 4 = 4
0 * 2^1 = 0 * 2 = 0
1 * 2^0 = 1 * 1 = 1

8 + 4 + 0 + 1 = 13
```

したがって、2進数 `1101` は10進数で `13` です。

#### 問題2

2進数 `10010` を10進数に変換してください。

#### 解答2

```
1 * 2^4 = 1 * 16 = 16
0 * 2^3 = 0 * 8 = 0
0 * 2^2 = 0 * 4 = 0
1 * 2^1 = 1 * 2 = 2
0  2^0 = 0 * 1 = 0

16 + 0 + 0 + 2 + 0 = 18
```

したがって、2進数 `10010` は10進数で `18` です。

### まとめ

2進数を10進数に変換するには、各ビットにその位置の重みを掛けて足し合わせる方法が基本です。この記事の例題を参考に、練習してみてください。
