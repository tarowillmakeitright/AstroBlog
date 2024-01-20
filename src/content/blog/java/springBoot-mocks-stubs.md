---
author: Taro Gray
pubDatetime: 2024-01-20T23:59:00.00Z
title: Spring Boot スタブ、モック、そしてJUnitの世界！
postSlug: springBoot-mocks-stubs
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Spring Boot
  - stubs
  - mocks
description: 皆さん、Spring Bootのテストの世界へようこそ！今日は、テスト中によく使用される「スタブ」と「モック」、そしてこれらを活用するJUnitについて探検します。面白くてわかりやすい例を交えながら、テストの旅を楽しんでいきましょう。
---

## Table of contents

皆さん、Spring Bootのテストの世界へようこそ！今日は、テスト中によく使用される「スタブ」と「モック」、そしてこれらを活用するJUnitについて探検します。面白くてわかりやすい例を交えながら、テストの旅を楽しんでいきましょう。

## スタブとモックって何？

テストの世界では、実際のオブジェクトやプロセスを模倣する「スタブ」と「モック」がよく使われます。これらはテストを単純化し、一貫した結果を得るために役立ちます。

- **スタブ**: テスト対象の外部依存部分を置き換える単純な実装。特定の入力に対して予め定義された応答を返します。
- **モック**: スタブよりも複雑で、期待される動作（メソッドが呼ばれた回数や順序など）を確認するのに使用されます。

## シナリオ: 宇宙飛行士の訓練

想像してみてください。宇宙飛行士が宇宙船の操作を学ぶためのシミュレーターを作成しています。実際の宇宙船を使う代わりに、スタブとモックを使用してシミュレーション環境を構築します。

### スタブの例: 太陽系スタブ

```java
public class SolarSystemStub implements SolarSystem {
    @Override
    public boolean isPlanet(String name) {
        return "Earth".equals(name);
    }
}
```

このスタブは、システムが地球を認識できるかどうかをテストするために使用されます。

### モックの例: 通信システムモック

```java
public class CommunicationSystemMock extends CommunicationSystem {
    private int messageCount = 0;

    @Override
    public void sendMessage(String message) {
        messageCount++;
    }

    public int getMessageCount() {
        return messageCount;
    }
}
```

このモックは、宇宙飛行士が正しい数のメッセージを送信しているかをテストするために使用されます。

## JUnitでテストを書く

JUnitは、Javaのテストフレームワークで、スタブやモックと組み合わせて使用されます。

```java
public class SpaceSimulatorTest {

    private SolarSystem solarSystem;
    private CommunicationSystem communicationSystem;

    @BeforeEach
    public void setUp() {
        solarSystem = new SolarSystemStub();
        communicationSystem = new CommunicationSystemMock();
    }

    @Test
    public void testPlanetRecognition() {
        assertTrue(solarSystem.isPlanet("Earth"));
    }

    @Test
    public void testCommunication() {
        communicationSystem.sendMessage("Hello Earth");
        assertEquals(1, ((CommunicationSystemMock) communicationSystem).getMessageCount());
    }
}
```

## リンクと参考文献

- [JUnit 5 User Guide](https://junit.org/junit5/docs/current/user-guide/) - JUnit 5の公式ユーザーガイド。
- [Baeldung on Mocks and Stubs](https://www.baeldung.com/java-stubs-mocks) - スタブとモックに関する詳細な解説。

## まとめ

スタブとモックを使用することで、テストの複雑さを減らし、より一貫した結果を得ることができます。JUnitと組み合わせることで、Spring Bootアプリケーションの信頼性を高める効果的なテストを作成できます。
