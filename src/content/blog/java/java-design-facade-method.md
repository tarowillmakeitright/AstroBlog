---
author: Taro Gray
pubDatetime: 2024-04-27T12:55:00.00Z
title: Java Design Pattern Facade Method について
postSlug: java-design-facade-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Facade Method
description: Facade パターンは、一連のインターフェースに対する単一の統一されたインターフェースを提供することで、複雑なシステムをより簡単に利用できるようにするデザインパターンです。このパターンは特に、大規模で複雑なソフトウェアシステムにおいて便利で、クライアントから見た時のシステムの複雑さを減らし、システムの利用をより簡単にします。
---

## Table of contents

## パターンの構造

1. **Facade (ファサード)**: クライアントから要求を受け、適切なサブシステムのメソッドを呼び出して応答します。ファサードはサブシステムの操作に必要なすべての複雑さを隠蔽します。
2. **Subsystems (サブシステム)**: ファサードの背後にあるサブシステムは、システムの実際の機能を担当します。これらはファサードを通じてのみアクセスされ、直接クライアントとはやりとりしません。

## Facade パターンの利点

- **単純化**: クライアントは複数のサブシステムと直接やりとりする代わりに、単一のインターフェースを通じて操作を行うことができます。
- **疎結合**: ファサードがサブシステムとのすべての対話を担当するため、システムの他の部分とサブシステムとの結合度が低くなります。
- **保守性の向上**: サブシステムの内部実装が変更されても、ファサードインターフェースが変わらなければクライアントコードはそのままで済むため、システムの保守が容易になります。

## 実装例

```java
public class HomeTheaterFacade {
    private Amplifier amp;
    private Tuner tuner;
    private DvdPlayer dvd;
    private Projector projector;

    public HomeTheaterFacade(Amplifier amp, Tuner tuner, DvdPlayer dvd, Projector projector) {
        this.amp = amp;
        this.tuner = tuner;
        this.dvd = dvd;
        this.projector = projector;
    }

    public void watchMovie(String movie) {
        System.out.println("Get ready to watch a movie...");
        projector.on();
        projector.wideScreenMode();
        amp.on();
        amp.setDvd(dvd);
        amp.setSurroundSound();
        amp.setVolume(5);
        dvd.on();
        dvd.play(movie);
    }

    public void endMovie() {
        System.out.println("Shutting movie theater down...");
        projector.off();
        amp.off();
        dvd.stop();
        dvd.eject();
        dvd.off();
    }
}

// Subsystem classes
class Amplifier {
    public void on() {}
    public void setDvd(DvdPlayer dvd) {}
    public void setSurroundSound() {}
    public void setVolume(int level) {}
    public void off() {}
}

class Tuner {}

class DvdPlayer {
    public void on() {}
    public void play(String movie) {}
    public void stop() {}
    public void eject() {}
    public void off() {}
}

class Projector {
    public void on() {}
    public void wideScreenMode() {}
    public void off() {}
}
```

## 関連記事

Facade パターンについてさらに学びたい場合は、以下の記事が役立ちます：

1. **Refactoring Guru** - [Facade Pattern](https://refactoring.guru/design-patterns/facade)
   - この記事では、Facade パターンの詳細な説明、利点

、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Facade Design Pattern](https://sourcemaking.com/design_patterns/facade)
   - Facade パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介しています。
