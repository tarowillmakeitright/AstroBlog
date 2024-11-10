---
author: Taro Gray
pubDatetime: 2024-11-10T12:00:00.00Z
title: "Spring BootでWebjarsを使用してThymeleafでフロントエンドを管理する方法"
postSlug: spring-boot-webjars-thymeleaf-integration
featured: true
draft: false
ogImage: "https://example.com/path/to/image.jpg" # 任意のURLに置き換えてください
tags:
  - Spring Boot
  - Webjars
  - Thymeleaf
  - Maven
description: "Spring BootでWebjarsを利用して、フロントエンドライブラリをCDNなしでローカル管理し、Thymeleafと連携する方法を解説します。"
---

## Table of Contents

## Introduction

Spring BootでWebjarsを利用することで、フロントエンドのライブラリ（BootstrapやjQueryなど）をプロジェクト内でローカル管理でき、CDNの依存を避けつつ静的アセットとして提供することができます。この記事では、Webjars公式サイトから必要なライブラリを追加し、Thymeleafと連携してローカルリソースを参照する方法を解説します。

## Webjars依存関係を追加する

Webjarsの依存関係を追加するには、pom.xmlに必要なライブラリを記述します。以下は、BootstrapとjQueryを例にしています。

```
<dependency>
    <groupId>org.webjars</groupId>
    <artifactId>bootstrap</artifactId>
    <version>5.1.3</version> <!-- バージョンを指定 -->
</dependency>

<dependency>
    <groupId>org.webjars</groupId>
    <artifactId>jquery</artifactId>
    <version>3.6.0</version> <!-- jQueryのバージョン -->
</dependency>
```

Webjars公式サイトから、他のフロントエンドライブラリも簡単に追加できます。追加したいライブラリを検索し、Maven用のコードをコピーしてpom.xmlに貼り付けます。

WebjarsのリソースをThymeleafで参照する

Webjarsのリソースは、Spring Bootでは自動的に/webjars/\*\*としてマッピングされます。Thymeleafテンプレートで、以下のようにth:href属性を使ってリソースを参照できます。

```
<!DOCTYPE html>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Webjars Example</title>
    <link rel="stylesheet" th:href="@{/webjars/bootstrap/5.1.3/css/bootstrap.min.css}" />
    <script th:src="@{/webjars/jquery/3.6.0/jquery.min.js}"></script>
</head>
<body>
    <h1 class="text-center">Hello, Webjars!</h1>
</body>
</html>
```

この例では、BootstrapのCSSとjQueryのJavaScriptを読み込んでいます。必要なバージョンやファイルパスを@{/webjars/...}の中で指定することで、ThymeleafとWebjarsの連携が簡単に行えます。

## アプリケーションを起動して確認

アプリケーションを起動し、設定したページを開いてフロントエンドリソースが正しく読み込まれているか確認します。エラーが発生した場合は、pom.xmlで指定したバージョンやHTML内のパスに誤りがないか確認してください。

## バージョン管理とアップデート

Webjarsを使用すると、依存関係はすべてpom.xmlで管理されるため、フロントエンドライブラリのバージョン管理が簡単になります。バージョンを明示することで、必要に応じてアップグレードやバージョンの固定も容易に行えます。

## Conclusion

Spring BootでWebjarsを使用すると、プロジェクト内でCDNに頼らずフロントエンドライブラリをローカル管理し、Thymeleafと連携して簡単に参照できます。これにより、ネットワーク接続に左右されずにリソースを確実に提供できるため、ローカル環境でも一貫した開発が可能です。
