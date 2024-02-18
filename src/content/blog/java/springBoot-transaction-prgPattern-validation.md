---
author: Taro Gray
pubDatetime: 2024-02-18T15:31:00.00Z
title: Spring Boot:トランザクション管理、PRGパターン、バリデーション
postSlug: springBoot-transaction-prgPattern-validation
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Spring Boot
  - transaction
  - prg pattern
  - validataion
description: これらの概念を適用することで、ユーザーエクスペリエンスを向上させ、データの整合性を保ちながら、堅牢なSpring Bootアプリケーションを構築できます。
---

## Table of contents

Spring Bootは、Javaのエコシステムで最も人気のあるフレームワークの一つです。このブログでは、Spring Bootでのトランザクション管理、Post/Redirect/Get (PRG) パターンの実装、そしてフォームバリデーションの方法について解説します。これらの概念を理解し、適用することで、堅牢でユーザーフレンドリーなWebアプリケーションを構築できます。

## トランザクション管理

Spring Frameworkは、宣言的トランザクション管理をサポートしており、これにより開発者はビジネスロジックに集中できます。`@Transactional` アノテーションをメソッドに付与するだけで、そのメソッドをトランザクションの境界として定義できます。

### コード例

```java
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
public class BookService {

    @Transactional
    public void addBook(Book book) {
        // ここでのデータベース操作は、全て同一トランザクション内で行われます
    }
}
```

この例では、`addBook` メソッド内で発生する全てのデータベース操作が、単一のトランザクション内で実行されます。これにより、処理中に例外が発生した場合、変更はロールバックされます。

## PRGパターン

Post/Redirect/Get (PRG) パターンは、Webアプリケーションで一般的な問題を解決します。フォーム送信後にリロードすると、同じデータが再送信されることを防ぎます。

### コード例

```java
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.servlet.mvc.support.RedirectAttributes;

@Controller
public class BookController {

    @PostMapping("/addBook")
    public String addBook(Book book, RedirectAttributes redirectAttributes) {
        // ここでbookを保存するロジック
        redirectAttributes.addFlashAttribute("message", "Book added successfully");
        return "redirect:/books";
    }
}
```

この例では、フォーム送信後に`/books`にリダイレクトし、二重送信の問題を解決しています。

## バリデーション

Spring Bootは、Bean Validation APIをサポートしており、モデル属性に対するバリデーションルールを簡単に定義できます。

### コード例

```java
import javax.validation.constraints.NotBlank;

public class Book {

    @NotBlank(message = "Title is required")
    private String title;

    // getterとsetter
}
```

そして、コントローラーで`@Valid`または`@Validated`アノテーションを使用してモデルを検証します。

```java
import org.springframework.validation.BindingResult;

@PostMapping("/addBook")
public String addBook(@Valid Book book, BindingResult result, RedirectAttributes redirectAttributes) {
    if (result.hasErrors()) {
        return "bookForm";
    }
    // 保存ロジック
    return "redirect:/books";
}
```

## リンクと参考文献

- [Spring Transaction Management](https://docs.spring.io/spring-framework/docs/current/reference/html/data-access.html#transaction)
- [Redirect After Post](https://en.wikipedia.org/wiki/Post/Redirect/Get)
- [Bean Validation with Spring Boot](https://reflectoring.io/bean-validation-with-spring-boot/)
