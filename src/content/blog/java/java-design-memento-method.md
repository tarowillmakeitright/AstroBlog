---
author: Taro Gray
pubDatetime: 2024-04-27T13:15:00.00Z
title: Java Design Pattern Memento Method について
postSlug: java-design-memento-method
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Java Design Pattern
  - Memento Method
description: Memento パターンは、オブジェクトの現在の状態を捕捉し、この状態を外部に保存して後でこの状態にオブジェクトを復元するためのデザインパターンです。このパターンは特に、アンドゥ機能やリセット機能を必要とするアプリケーションで有効です。
---

## Table of contents

## パターンの構成要素

1. **Originator**: 状態を持ち、Memento オブジェクトを使用して状態を保存または復元するオブジェクト。
2. **Memento**: Originator の内部状態を保存するオブジェクト。外部からはこの状態にアクセスできず、Originator 自身のみがアクセスできます。
3. **Caretaker**: Memento を保存する役割を持ち、いつどの Memento を使って Originator の状態を復元するかを決定しますが、Memento の内容にはアクセスしません。

## Memento パターンの利点

- **カプセル化の保持**: Memento パターンは、状態を持つオブジェクトのカプセル化を侵害することなく、その状態を保存・復元する機能を提供します。
- **履歴管理の柔軟性**: いつでも任意の時点の状態に戻ることが可能です。
- **高い再現性と信頼性**: エラーが発生した場合やユーザーが変更を取り消したい場合に、安全に元の状態に復元できます。

## 実装例

```java
// Originator
class Editor {
    private String content;

    public void setContent(String content) {
        this.content = content;
    }

    public String getContent() {
        return content;
    }

    public EditorMemento save() {
        return new EditorMemento(content);
    }

    public void restore(EditorMemento memento) {
        content = memento.getContent();
    }
}

// Memento
class EditorMemento {
    private final String content;

    public EditorMemento(String content) {
        this.content = content;
    }

    private String getContent() {
        return content;
    }
}

// Caretaker
public class EditorCaretaker {
    private List<EditorMemento> saves = new ArrayList<>();

    public void addMemento(EditorMemento m) {
        saves.add(m);
    }

    public EditorMemento getMemento(int index) {
        return saves.get(index);
    }
}

// Client
public class MementoDemo {
    public static void main(String[] args) {
        Editor editor = new Editor();
        EditorCaretaker caretaker = new EditorCaretaker();

        editor.setContent("First");
        caretaker.addMemento(editor.save());
        editor.setContent("Second");

        editor.restore(caretaker.getMemento(0));
        System.out.println(editor.getContent()); // Output: First
    }
}
```

## 関連記事

Memento パターンについてさらに学びたい場合は、以下の記事が役立ちます：

1. **Refactoring Guru** - [Memento Pattern](https://refactoring.guru/design-patterns/memento)

   - この記事では、Memento パターンの詳細な説明、利点、欠点、さらには多言語での実装例が提供されています。

2. **SourceMaking** - [Memento Design Pattern](https://sourcemaking.com/design_patterns/memento)
   - Memento パターンの背景、動機、構造について詳しく説明しており、実際の使用例も紹介しています。
