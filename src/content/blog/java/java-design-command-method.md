---
author: Taro Gray
pubDatetime: 2024-04-27T14:18:00.00Z
title: Java Design Pattern Command Method について
postSlug: java-design-command-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Command Method
description: Command パターンは、要求自体をカプセル化することで、要求を発行するオブジェクトと要求を実行するオブジェクトを分離するデザインパターンです。このパターンを使用することで、操作の実行、キャンセル、ログ記録、トランザクションの管理などが容易になります。特にユーザーインターフェイスやトランザクションシステムにおいて有効です。
---

## Table of contents

## パターンの構成要素

1. **Command**: 実行する操作に関連したすべての情報を持つインターフェース。通常は `execute()` メソッドを一つだけ持ちます。
2. **Concrete Command**: Command インターフェースを実装し、特定の動作をカプセル化します。
3. **Client**: Command オブジェクトを生成し、Receiver を設定します。
4. **Invoker**: Command オブジェクトを受け取り、それを実行します。
5. **Receiver**: 実際の操作を実行するオブジェクトです。

## Command パターンの利点

- **柔軟性の向上**: 新しい Command クラスを追加することで、既存のクラスを変更することなく新しい命令を簡単に追加できます。
- **再利用性**: 同じ命令を多くの異なるコンテキストで再利用することができます。
- **操作の分離**: 実行する操作とその実行を管理するクラスを分離することができます。

## 実装例

```java
// Command interface
interface Command {
    void execute();
}

// Receiver class
class Light {
    public void turnOn() {
        System.out.println("The light is on");
    }

    public void turnOff() {
        System.out.println("The light is off");
    }
}

// Concrete Command
class TurnOnCommand implements Command {
    private Light light;

    public TurnOnCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.turnOn();
    }
}

class TurnOffCommand implements Command {
    private Light light;

    public TurnOffCommand(Light light) {
        this.light = light;
    }

    public void execute() {
        light.turnOff();
    }
}

// Invoker class
class RemoteControl {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void pressButton() {
        command.execute();
    }
}

// Client
public class CommandDemo {
    public static void main(String[] args) {
        Light light = new Light();
        Command turnOn = new TurnOnCommand(light);
        Command turnOff = new TurnOffCommand(light);

        RemoteControl remote = new RemoteControl();
        remote.setCommand(turnOn);
        remote.pressButton();
        remote.setCommand(turnOff);
        remote.pressButton();
    }
}
```

## 関連記事

Command パターンについてさらに学びたい場合は、以下の記事が役立ちます：

1. **Refactoring Guru** - [Command Pattern](https://refactoring.guru/design-patterns/command)

   - この記事では、Command パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Command Design Pattern](https://sourcemaking.com/design_patterns/command)
   - Command パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介しています。
