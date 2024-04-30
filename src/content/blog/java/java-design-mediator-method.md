---
author: Taro Gray
pubDatetime: 2024-04-27T13:06:00.00Z
title: Java Design Pattern Mediator Method について
postSlug: java-design-mediator-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Mediator Method
description: Mediator パターンは、オブジェクト間の複雑な通信を管理し、疎結合を促進するデザインパターンです。このパターンでは、オブジェクト間の直接的な通信を避け、代わりに Mediator オブジェクトを通じて交流することで、システム内の各オブジェクトが他のオブジェクトと独立して操作できるようになります。
---

## Table of contents

## パターンの構成要素

1. **Mediator**: すべてのコンポーネント間の通信を調整するインターフェースを提供します。
2. **Concrete Mediator**: Mediator インターフェースを実装し、具体的なコンポーネント間の通信を調整します。
3. **Colleague（同僚）クラス**: Mediator を通じて互いに通信するオブジェクト群です。

## Mediator パターンの利点

- **疎結合**: 各コンポーネントは他のコンポーネントと直接通信するのではなく、Mediator を介して通信するため、コンポーネント間の依存関係が減少します。
- **集中管理**: 通信ロジックが Mediator 一箇所に集中するため、システムの管理が容易になります。
- **拡張性**: 新しいコンポーネントを追加する際、既存のコードを変更せずに Mediator に組み込むだけで済むため、システムを容易に拡張できます。

### 実装例

```java
// Mediator interface
interface ChatMediator {
    void sendMessage(String msg, User user);
    void addUser(User user);
}

// Concrete Mediator
class ChatRoom implements ChatMediator {
    private List<User> users;

    public ChatRoom() {
        this.users = new ArrayList<>();
    }

    @Override
    public void addUser(User user) {
        this.users.add(user);
    }

    @Override
    public void sendMessage(String msg, User user) {
        for (User u : users) {
            // メッセージを送信者以外のすべてのユーザーに送信
            if (u != user) {
                u.receive(msg);
            }
        }
    }
}

// Colleague
abstract class User {
    protected ChatMediator mediator;
    protected String name;

    public User(ChatMediator med, String name) {
        this.mediator = med;
        this.name = name;
    }

    public abstract void send(String msg);
    public abstract void receive(String msg);
}

// Concrete Colleague
class ConcreteUser extends User {
    public ConcreteUser(ChatMediator med, String name) {
        super(med, name);
    }

    @Override
    public void send(String msg) {
        System.out.println(this.name + ": Sending Message = " + msg);
        mediator.sendMessage(msg, this);
    }

    @Override
    public void receive(String msg) {
        System.out.println(this.name + ": Received Message = " + msg);
    }
}

// Client
public class MediatorDemo {
    public static void main(String[] args) {
        ChatMediator mediator = new ChatRoom();
        User user1 = new ConcreteUser(mediator, "John");
        User user2 = new ConcreteUser(mediator, "Doe");
        mediator.addUser(user1);
        mediator.addUser(user2);

        user1.send("Hi there!");
    }
}
```

## 関連記事

Mediator パターンについてさらに学びたい場合は、以下の記事が役立ちます：

1. **Refactoring Guru** - [Mediator Pattern](https://refactoring.guru/design-patterns/mediator)

   - この記事では、Mediator パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Mediator Design Pattern](https://sourcemaking.com/design_patterns/mediator)
   - Mediator パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介
