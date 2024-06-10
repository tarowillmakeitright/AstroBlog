---
author: Taro Gray
pubDatetime: 2024-05-13T12:00:00.00Z
title: Spring JDBCを用いたデータベースからのデータ取得方法
postSlug: fetching-data-with-spring-jdbc
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Spring
  - JDBC
description: Spring JDBCのJdbcTemplateを使用して、データベースからデータを効率的に取得する方法を詳しく解説します。エンティティオブジェクト、マップオブジェクトへの変換、そして複数レコードの取得について具体的な例を交えて説明します。
---

## Table of Contents

## JdbcTemplateとは

Spring JDBCの核となるのがJdbcTemplateです。これは、JDBCの冗長なコードを省略し、データベース操作を簡素化するためのSpringのテンプレートです。JdbcTemplateを使用することで、SQLクエリの実行、結果セットの取り扱い、例外のハンドリングなどが容易になります。

## レコードをEntityオブジェクトに変換して取得する方法

エンティティクラス `Training` が定義されており、このクラスのインスタンスとしてデータベースから取得したデータをマッピングすることができます。以下のように `queryForObject` メソッドを使用します。

```java
Training training = jdbcTemplate.queryForObject(
    "SELECT * FROM training WHERE id = ?",
    new DataClassRowMapper<>(Training.class),
    "t01"
);
```

このメソッドは、指定されたSQLクエリを実行し、結果を `Training` クラスのインスタンスにマッピングします。ここで、`DataClassRowMapper` はSpringが提供する汎用的なRowMapper実装で、結果セットの行を指定されたクラスのインスタンスにマッピングするために使用されます。

## レコードをMapオブジェクトに変換して取得する方法

SQLクエリの結果を `Map<String, Object>` の形式で取得するには、`queryForMap` メソッドを使用します。

```java
Map<String, Object> map = jdbcTemplate.queryForMap(
    "SELECT * FROM training WHERE id = ?",
    "t01"
);
```

このメソッドは、クエリが返す行をキーと値のペアのマップとして返します。これにより、カラム名をキーとして使用して各データにアクセスすることが可能です。

## 複数レコードをEntityに変換して取得する方法

データベースから複数のレコードを取得し、それぞれを `Training` クラスのインスタンスにマッピングするには、`query` メソッドを使用します。

```java
List<Training> trainings = jdbcTemplate.query(
    "SELECT * FROM training",
    new DataClassRowMapper<>(Training.class)
);
```

このメソッドは、SQLクエリを実行し、結果セットの各行を `Training` クラスのインスタンスにマッピングしたリストを返します。これにより、複数のレコードを効率的
