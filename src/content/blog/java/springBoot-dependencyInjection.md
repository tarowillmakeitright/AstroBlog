---
author: Taro Gray
pubDatetime: 2024-01-07T12:58:00.00Z
title: Spring Boot 馬鹿げた例で学ぶ依存性注入！
postSlug: springBoot-dependencyInjection
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Spring Boot
description: 依存性注入は、オブジェクトの作成と使用を分離する設計パターンです。これにより、コードはよりモジュラーになり、テストしやすく、メンテナンスも容易になります。では、どのように動くのでしょうか？面白い例で見てみましょう！
---

## Table of contents

## Spring Boot: 馬鹿げた例で学ぶ依存性注入！

## 依存性注入って？

依存性注入は、オブジェクトの作成と使用を分離する設計パターンです。これにより、コードはよりモジュラーになり、テストしやすく、メンテナンスも容易になります。では、どのように動くのでしょうか？面白い例で見てみましょう！

## 馬鹿げた例で理解する

想像してください。あなたは宇宙船のキャプテンです。あなたの宇宙船は、星間旅行に必要な多くのシステムを持っています。これらのシステムはすべて互いに依存していますが、個々には直接手を出せません。ここで依存性注入が登場します！

```java
@Component
public class Spaceship {
    @Autowired
    private Engine engine;
    @Autowired
    private Shield shield;

    public void startJourney() {
        engine.start();
        shield.activate();
        System.out.println("Adventure begins!");
    }
}

@Component
public class Engine {
    public void start() {
        System.out.println("Engine started!");
    }
}

@Component
public class Shield {
    public void activate() {
        System.out.println("Shield activated!");
    }
}
```
