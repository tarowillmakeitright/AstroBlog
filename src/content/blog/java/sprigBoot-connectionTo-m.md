---
author: Taro Gray
pubDatetime: 2024-01-07T13:20:00.00Z
title: Spring BootでMySQLに接続し、HTMLにデータを表示する冒険！
postSlug: sprigBoot-connectionTo-mysql
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Spring Boot
  - Thymeleaf
  - MySQL
description: このブログはSpring Bootを使用したMySQLデータベース接続とHTMLへのデータ表示を中級者向けに解説しており、コード例を交えながらステップバイステップでプロセスを説明しています。読者が興味を持ちながら理解を深められるように、わかりやすさを優先しています。また、更なる学びのためのリンクや参考文献も提供しています。
---

## Table of contents

## Spring BootでMySQLに接続し、HTMLにデータを表示する冒険！

## Spring BootとMySQLの連携

Spring BootアプリケーションでMySQLデータベースに接続するには、まず依存関係をセットアップし、データベースの設定をアプリケーションに伝える必要があります。

### 依存関係の追加

`pom.xml`ファイルに以下の依存関係を追加します。

```xml
<dependencies>
    <!-- MySQLドライバ -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <scope>runtime</scope>
    </dependency>
    <!-- Spring Boot Web スターター -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <!-- Spring Boot Data JPA スターター -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
</dependencies>
```

### application.propertiesの設定

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/db_example
spring.datasource.username=dbuser
spring.datasource.password=dbpass
spring.jpa.hibernate.ddl-auto=update
```

## モデルとリポジトリの作成

次に、データを表すモデルクラスと、データを操作するリポジトリインターフェースを作成します。

### モデルクラスの例

```java
@Entity
public class Book {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private Long id;

    private String title;
    private String author;

    // ゲッターとセッター...
}
```

### リポジトリインターフェースの例

```java
public interface BookRepository extends JpaRepository<Book, Long> {
    List<Book> findByAuthor(String author);
}
```

## コントローラーの作成

データを取得し、HTMLビューに渡すためのコントローラーを作成します。

```java
@Controller
public class BookController {

    @Autowired
    private BookRepository bookRepository;

    @GetMapping("/books")
    public String getAllBooks(Model model) {
        model.addAttribute("books", bookRepository.findAll());
        return "books";
    }
}
```

## HTMLビューの作成

Thymeleafを使って、データを表示するHTMLビューを作成します。

```html
<!doctype html>
<html xmlns:th="http://www.thymeleaf.org">
  <head>
    <title>Books</title>
  </head>
  <body>
    <h1>Book List</h1>
    <ul>
      <li th:each="book : ${books}">
        <span th:text="${book.title}">Book Title</span> by
        <span th:text="${book.author}">Author</span>
      </li>
    </ul>
  </body>
</html>
```

## リンクと参考文献

- [Spring Boot Documentation](https://spring.io/projects/spring-boot) - 公式のSpring Bootドキュメント。
- [Spring Data JPA Documentation](https://spring.io/projects/spring-data-jpa) - Spring Data JPAの詳細について学ぶ。
- [Thymeleaf Official Documentation](https://www.thymeleaf.org/documentation.html) - Thymeleafのテンプレートエンジンについての公式ドキュメント。

## まとめ

これで、あなたはSpring Bootを使ってMySQLデータベースに接続し、データをHTMLページに表示する方法を学びました。これはデータ駆動型のWebアプリケーションを作成する際の基礎であり、実際のプロジェクトに応用できる強力なスキルです。ぜひこの知識を使って、あなたのアプリケーションを構築し、ユーザーに素晴らしい体験を提供してください！
