---
author: Taro Gray
pubDatetime: 2024-05-19T16:33:00.000Z
title: Spring BootでのHttpStatusの活用方法
postSlug: springBoot-httpstatus
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Spring Boot
  - HttpStatus
description: Spring BootにおけるWebアプリケーション開発で、HttpStatusはHTTPレスポンスを効果的に管理するために重要です。この記事では、HttpStatus.CREATEDとその他のステータスコードの使用法を詳しく解説します。
---

## Table of contents

## イントロダクション

HTTPステータスコードは、Webサーバーからクライアントへのレスポンスの状態を示す重要な情報です。Spring BootでのAPI開発において、適切なHttpStatusを返すことは、効果的なコミュニケーションとエラー管理に不可欠です。

## HttpStatusとは

`HttpStatus` は、HTTP応答コードを表す一連の定数を提供するSpring Frameworkのクラスです。これらのステータスコードは、リクエストが成功したか、エラーが発生したか、その他の情報をクライアントに通知します。

## 主要なHttpStatusコード

以下は、Spring Bootでよく使用されるいくつかのHttpStatusコードです：

- **HttpStatus.CREATED (201)**: リソースが正常に作成されたことを示します。主にPOSTリクエストの結果として使用されます。
- **HttpStatus.OK (200)**: リクエストが成功し、クライアントに返されるデータがある場合に使用されます。
- **HttpStatus.NO_CONTENT (204)**: リクエストは成功したが、クライアントに返す内容がないことを示します。
- **HttpStatus.BAD_REQUEST (400)**: クライアントからのリクエストが不正または誤っているため、サーバーが処理できないことを示します。
- **HttpStatus.NOT_FOUND (404)**: 指定されたリソースがサーバー上に存在しないことを示します。
- **HttpStatus.INTERNAL_SERVER_ERROR (500)**: サーバー内の問題によりリクエストを処理できないことを示します。

## Spring Bootでの使用例

以下の例では、異なるHttpStatusを返す方法を示します。

```java
@RestController
public class BookController {

    @Autowired
    private BookService bookService;

    // リソースの作成
    @PostMapping("/books")
    public ResponseEntity<Book> createBook(@RequestBody Book book) {
        Book savedBook = bookService.save(book);
        return ResponseEntity.status(HttpStatus.CREATED).body(savedBook);
    }

    // リソースの取得
    @GetMapping("/books/{id}")
    public ResponseEntity<Book> getBookById(@PathVariable Long id) {
        return bookService.findById(id)
                .map(book -> ResponseEntity.ok(book))
                .orElseGet(() -> ResponseEntity.notFound().build());
    }
}
```

このコードでは、新しい書籍を作成した際にはHttpStatus.CREATEDを、書籍が見つかった場合にはHttpStatus.OKを、見つからない場合にはHttpStatus.NOT_FOUNDを返しています。

## 結論

適切なHttpStatusコードを返すことで、APIの利用者に明確な情報を提供し、エラーハンドリングを効果的に行うことができます。HttpStatusを適切に活用することは、Spring BootでのAPI開発の成功には不可
