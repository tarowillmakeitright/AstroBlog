---
author: Taro Gray
pubDatetime: 2024-01-28T16:02:00.00Z
title: Javaの鍵 save()とdeleteById()の使い方
postSlug: java-save-deleteById
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
description: save()と deleteById() は、Javaでのデータベース操作における基本的かつ強力なツールです。これらのメソッドを使いこなすことで、アプリケーションのデータ管理を効率的かつ効果的に行うことができます。ぜひこれらのメソッドを活用して、あなたのアプリケーションを強化しましょう！
---

## Table of contents

こんにちは、Javaの世界のマスターたち！今日は、データ永続化の基本である`save()`と`deleteById()`メソッドに焦点を当てます。これらのメソッドは、データベースとのやり取りにおいて不可欠なツールです。それでは、中級者向けの具体例を交えて、この冒険を始めましょう。

## `save()`メソッド

`save()`メソッドは、エンティティをデータベースに保存するために使われます。新しいデータを作成する場合や、既存のデータを更新する場合に使用されます。

## `deleteById()`メソッド

`deleteById()`メソッドは、指定されたIDを持つエンティティをデータベースから削除するために使われます。このメソッドは、エンティティが存在しない場合には何もしません。

## コード例：魔法の図書館システム

想像してみてください、あなたは魔法の図書館の管理システムを作成しています。図書館では、新しい魔法の書物を追加したり、古い書物を削除したりする必要があります。

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;
import java.util.Optional;

@Service
public class LibraryService {

    @Autowired
    private BookRepository bookRepository;

    // 書物を保存
    public Book saveBook(Book book) {
        return bookRepository.save(book);
    }

    // 書物を削除
    public void deleteBookById(Long id) {
        bookRepository.deleteById(id);
    }
}

public interface BookRepository extends JpaRepository<Book, Long> {
    // JpaRepositoryのメソッドを使用
}

@Entity
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;
    private String title;

    // コンストラクタ、ゲッター、セッター
}
```

この例では、`LibraryService`クラスが書物の保存と削除を担当します。`saveBook`メソッドは新しい書物を保存し、`deleteBookById`メソッドは指定されたIDの書物を削除します。

## リンクと参考文献

- [Spring Data JPA Documentation](https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#repositories) - Spring Data JPAの公式ドキュメント。
- [Baeldung on Spring Data Repositories](https://www.baeldung.com/spring-data-repositories) - Spring Dataリポジトリに関する詳細なガイド。
