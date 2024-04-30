---
author: Taro Gray
pubDatetime: 2024-01-28T21:58:00.00Z
title: Spring Bootの例外処理の魔法：@ControllerAdvice, @ResponseBody, @ExceptionHandler, @ResponseStatus
postSlug: sprigBoot-controllerAdvice-responseBody-responseStatus
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Spring Boot
description: ControllerAdvice, @ResponseBody, @ExceptionHandler, @ResponseStatus(HttpStatus.NOT_FOUND)は、Spring Bootアプリケーションにおける例外処理を強化するための鍵です。これらのアノテーションを使いこなすことで、エラー処理をより効率的に、かつユーザーフレンドリーに行うことができます。エラー処理の魔法を使って、あなたのアプリケーションをより堅牢なものにしましょう！
---

## Table of contents

こんにちは、Spring Bootの世界の探求者たち！今日はSpring Bootの例外処理の魔法について掘り下げていきます。具体的には、`@ControllerAdvice`, `@ResponseBody`, `@ExceptionHandler`, そして`@ResponseStatus(HttpStatus.NOT_FOUND)`の4つのアノテーションに焦点を当てます。これらは、アプリケーションのエラー処理を効率化し、より堅牢なシステムを構築するための重要なツールです。それでは、中級者向けの具体例を交えて、この冒険を始めましょう。

## Spring Bootの例外処理

Spring Bootでは、例外処理を簡単かつ効果的に行うためのいくつかのアノテーションが用意されています。これらのアノテーションを使用することで、エラー処理のロジックを集中化し、コードの再利用性と可読性を向上させることができます。

## @ControllerAdvice

`@ControllerAdvice`は、複数のコントローラーにまたがる例外処理や、データバインディング、データフォーマットの設定を一元管理するために使用されます。

## @ResponseBody

`@ResponseBody`は、コントローラーのメソッドがHTTPレスポンスのボディに直接書き込むべきデータを返すことを示します。

## @ExceptionHandler

`@ExceptionHandler`は、特定の例外を処理するメソッドに使用されます。このアノテーションが付与されたメソッドは、指定された例外が発生したときに自動的に呼び出されます。

## @ResponseStatus

### (HttpStatus.NOT_FOUND)

`@ResponseStatus(HttpStatus.NOT_FOUND)`は、HTTPレスポンスとして特定のステータスコード（この場合は404 Not Found）を返すことを指示します。

## コード例：カスタム例外ハンドラ

想像してみてください、あなたはユーザー情報を扱うWebアプリケーションを作成しており、特定のユーザーが見つからない場合にカスタムのエラーメッセージを返したいと考えています。

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ResponseBody
    @ExceptionHandler(UserNotFoundException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public String userNotFoundHandler(UserNotFoundException ex) {
        return ex.getMessage();
    }
}

public class UserNotFoundException extends RuntimeException {

    public UserNotFoundException(String userId) {
        super("User not found with id: " + userId);
    }
}
```

この例では、`UserNotFoundException`が発生した場合に、`userNotFoundHandler`メソッドが呼び出され、404 Not Foundのステータスコードと共にカスタムのエラーメッセージが返されます。

## リンクと参考文献

- [Spring Boot Documentation](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/) - Spring Bootの公式ドキュメント。
- [Baeldung on @ControllerAdvice and @ExceptionHandler](https://www.baeldung.com/exception-handling-for-rest-with-spring) - SpringでRESTful APIの例外処理を行う方法に関するガイド。
