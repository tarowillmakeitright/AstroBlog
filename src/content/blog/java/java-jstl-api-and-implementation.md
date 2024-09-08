---
author: Taro Gray
pubDatetime: 2024-09-02T21:00:00.00Z
title: JSTL APIと実装の違いと、JSTLを正しく使うために必要なJARファイル
postSlug: java-jstl-api-and-implementation
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - JSTL
description: JSTL（JavaServer Pages Standard Tag Library）を使うには、APIと実装の両方が必要です。これらの違いと正しい設定方法について解説します。
---

## Table of contents

## 1. JSTLとは？

JSTL（JavaServer Pages Standard Tag Library）は、JSPページ内でよく使用される共通のタスク（ループ処理、条件分岐、フォーマット、国際化など）を簡単に実装できるようにする標準タグライブラリです。JSTLを使用することで、スクリプトレット（Javaコード）をJSPに直接記述する必要がなくなり、コードの可読性とメンテナンス性が向上します。

## 2. JSTLを使うには何が必要か？

JSTLを正しく動作させるには、プロジェクトに2つの主要なJARファイルを追加する必要があります。

- **JSTL API JAR** (`jakarta.servlet.jsp.jstl-api.jar`)
  - JSTLタグの仕様や宣言が定義されています。たとえば、`<c:forEach>` や `<c:if>` などのタグがどう動作するかが記載されています。
- **JSTL Implementation JAR** (`jakarta.servlet.jsp.jstl.jar`)
  - 実際にタグが動作するための実装が含まれています。APIだけでは動作せず、この実装JARによって、JSTLタグが機能します。

両方のJARがないと、JSTLタグを使用してもエラーが発生します。APIは仕様だけを定義しており、実装がないとその仕様通りに動作するコードが存在しないからです。

## 3. JSTL APIと実装の違い

### JSTL API

- **役割**: JSTL APIは、タグライブラリのインターフェースや使用方法を定義します。`<c:forEach>` や `<c:if>` などのタグの動作がどうあるべきか（ループ処理、条件分岐など）の仕様が記載されています。
- **例**: APIは、「このタグはリストのすべての要素をループするために使われます」といった定義を提供します。

### JSTL Implementation

- **役割**: JSTL Implementationは、JSTL APIで定義された動作を実際に実装するJARです。APIが「こう動作すべき」と記述する仕様を、実際にその通りに動かすためのコードを含んでいます。

- **例**: `<c:forEach>` タグがリストのすべての要素を正しくループし、必要な処理を行うためのコードが実装されています。

### なぜ両方が必要か？

- **APIだけ**では、仕様やインターフェースだけが提供されるため、タグは動作しません。
- **実装だけ**では、タグの動作方法がわからないため、何をどう処理するかの指示が不足します。
- 両方が揃うことで、タグの仕様（API）とその仕様通りに動作するコード（実装）がセットになり、初めてJSTLが正常に動作します。

## 4. JSTLの設定方法

### Mavenプロジェクトでの設定

Mavenを使用している場合、`pom.xml` に以下の依存関係を追加して、JSTL APIと実装を一度に追加します。

```xml
<!-- JSTL API -->
<dependency>
    <groupId>jakarta.servlet.jsp.jstl</groupId>
    <artifactId>jakarta.servlet.jsp.jstl-api</artifactId>
    <version>3.0.0</version>
</dependency>

<!-- JSTL Implementation -->
<dependency>
    <groupId>org.glassfish.web</groupId>
    <artifactId>jakarta.servlet.jsp.jstl</artifactId>
    <version>3.0.0</version>
</dependency>
```

これで、Mavenが必要なJARファイルを自動的にダウンロードし、プロジェクトに追加します。

### Mavenを使用しない場合（手動でJARを追加）

Mavenを使用していない場合、以下のリンクからJARファイルをダウンロードし、プロジェクトの `WEB-INF/lib` フォルダに追加します。

- [JSTL API JAR](https://mvnrepository.com/artifact/jakarta.servlet.jsp.jstl/jakarta.servlet.jsp.jstl-api)
- [JSTL Implementation JAR](https://mvnrepository.com/artifact/org.glassfish.web/jakarta.servlet.jsp.jstl)

これにより、JSTLタグが正しく動作するようになります。

### JSPファイル内でのJSTLタグライブラリのインポート

以下のURIを使ってJSTLタグライブラリをインポートします。

```jsp
<%@ taglib uri="http://jakarta.ee/jsp/jstl/core" prefix="c" %>
<%@ taglib uri="http://jakarta.ee/jsp/jstl/fmt" prefix="fmt" %>
```

- **Coreタグライブラリ**: 条件分岐、ループ処理などを行う基本的なJSTLタグが含まれています。
- **Formatタグライブラリ**: 日付や数値のフォーマット、国際化を行うためのタグが含まれています。

## 5. まとめ

- JSTLを使用するには、**JSTL API** と **JSTL Implementation** の両方が必要です。これにより、JSPファイル内でJSTLタグを正しく使用できます。
- **JSTL API** は、タグの使用方法や仕様を定義しますが、これだけでは動作しません。**JSTL Implementation** がその動作を実際に実行するために必要です。

- JSTLをプロジェクトに追加する際には、Mavenを使う場合は `pom.xml` に依存関係を追加し、Mavenを使わない場合は手動でJARファイルを追加します。

JSTLを使うことで、JSP内のスクリプトレットを減らし、より簡潔でメンテナンスしやすいコードを書くことができます。
