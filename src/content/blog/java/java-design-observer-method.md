---
author: Taro Gray
pubDatetime: 2024-04-27T13:11:00.00Z
title: Java Design Pattern Observer Method について
postSlug: java-design-observer-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Observer Method
description: Observer パターンは、オブジェクト間の依存関係を最小限に抑えつつ、あるオブジェクトの状態の変化を他のオブジェクトに自動的に通知し、更新させるデザインパターンです。このパターンは、特にイベント駆動型のシステムやユーザーインターフェースのコンポーネント間でのデータの同期に適しています。
---

## Table of contents

## パターンの構成要素

1. **Subject**: 状態の変化を監視されるオブジェクト。Observer オブジェクトを登録、削除し、状態の変化があると通知します。
2. **Observer**: Subject の状態変化に応じて更新を行うインターフェース。Subject からの通知を受けて具体的な更新処理を実装します。
3. **ConcreteObserver**: Observer インターフェースの具体的な実装。Subject の状態変化を監視し、状態が変化すると更新されます。

## Observer パターンの利点

- **疎結合の促進**: Subject は Observer の詳細を知らず、Observer は自分が何を観察しているかのみを知っているため、お互いの独立性が保たれます。
- **動的なサブスクリプション**: オブジェクトはいつでも通知リストに登録したり解除したりすることができます。
- **再利用性の向上**: Subject や Observer を独立して再利用することが可能です。

## 実装例

```java
// Subject interface
interface Subject {
    void attach(Observer o);
    void detach(Observer o);
    void notifyUpdate(Message m);
}

// Concrete Subject
class NewsAgency implements Subject {
    private List<Observer> observers = new ArrayList<>();
    private String news;

    public void setNews(String news) {
        this.news = news;
        notifyUpdate(new Message(news));
    }

    @Override
    public void attach(Observer o) {
        observers.add(o);
    }

    @Override
    public void detach(Observer o) {
        observers.remove(o);
    }

    @Override
    public void notifyUpdate(Message m) {
        for (Observer o : observers) {
            o.update(m);
        }
    }
}

// Observer interface
interface Observer {
    void update(Message m);
}

// Concrete Observer
class NewsChannel implements Observer {
    private String news;

    @Override
    public void update(Message m) {
        this.news = m.getContent();
        System.out.println("NewsChannel updated with news: " + news);
    }
}

// Message class to carry news data
class Message {
    final private String content;

    public Message(String content) {
        this.content = content;
    }

    public String getContent() {
        return content;
    }
}

// Client
public class ObserverDemo {
    public static void main(String[] args) {
        NewsAgency observable = new NewsAgency();
        NewsChannel observer = new NewsChannel();

        observable.attach(observer);
        observable.setNews("Here is your latest news!");
    }
}
```

## 関連記事

Observer パターンについてさらに学びたい場合は、以下の記事が役立ちます：

1. **Refactoring Guru** - [Observer Pattern](https://refactoring.guru/design-patterns/observer)

   - この記事では、Observer パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Observer Design Pattern](https://sourcemaking.com/design_patterns/observer)
   - Observer パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介しています。

これら
