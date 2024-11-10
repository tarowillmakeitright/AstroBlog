---
author: Taro Gray
pubDatetime: 2024-11-10T13:00:00.00Z
title: "Spring BootでThymeleaf Layout Dialectを使ったレイアウトテンプレートの設定方法"
postSlug: thymeleaf-layout-template
featured: true
draft: false
tags:
  - Spring Boot
  - Thymeleaf
  - Layout Dialect
  - Webjars
description: "Spring BootでThymeleaf Layout Dialectを使ってレイアウトテンプレートを作成し、メインテンプレートからindex.htmlへ簡単にレイアウトを適用する方法を紹介します。"
---

## Table of Contents

    1.	Introduction
    2.	レイアウトテンプレートの作成 - layout/main.html
    3.	コンテンツの指定 - index.html
    4.	詳細なFragmentの使い方
    5.	Conclusion

## Introduction

Spring BootでThymeleafのLayout Dialectを使用することで、アプリケーション全体の統一的なレイアウトテンプレートを効率的に管理できます。この記事では、メインのテンプレートlayout/main.htmlを作成し、個別ページでこのレイアウトを簡単に適用する方法について説明します。

レイアウトテンプレートの作成 - layout/main.html

まず、layout/main.htmlファイルにアプリ全体で共通のレイアウトを記述します。このテンプレートでは、Bootstrap、Font Awesome、およびhtmxのWebjarsを使用して、スタイリングや機能を追加しています。

## layout/main.html

```
<!DOCTYPE html>
<html th:lang="|${#locale.language}-${#locale.country}|"
      xmlns:th="http://www.thymeleaf.org"
      xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout"
      data-bs-theme="dark">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>My Anime App</title>
    <link rel="stylesheet" th:href="@{/css/application.css}">
    <!-- Bootstrap CSS -->
    <link th:rel="stylesheet" th:href="@{/webjars/bootstrap/css/bootstrap.min.css}"/>
    <!-- Font Awesome -->
    <link th:rel="stylesheet" th:href="@{/webjars/font-awesome/css/all.min.css}"/>
    <script th:src="@{/webjars/htmx.org/dist/htmx.min.js}"></script>
    <!-- Bootstrap Bundle with Popper -->
    <script type="text/javascript" th:src="@{/webjars/bootstrap/js/bootstrap.bundle.min.js}"></script>
</head>

<body>
    <header>
        <!-- ヘッダーの内容 -->
    </header>

    <main layout:fragment="content">
        <!-- 子ページごとのコンテンツがここに配置されます -->
    </main>

    <footer>
        <!-- フッターの内容 -->
    </footer>
</body>
</html>
```

このテンプレートには、アプリケーション全体で使用されるヘッダー、フッターが含まれています。layout:fragment="content"で指定された部分に、個別ページからのコンテンツが挿入されます。

コンテンツの指定 - index.html

個別のページ（ここではindex.html）で、このlayout/main.htmlテンプレートを適用するには、layout:decorate属性を使って親テンプレートを指定します。

index.html

```
<!DOCTYPE html>
<html lang="en"
      xmlns:th="http://www.thymeleaf.org"
      xmlns:layout="http://www.ultraq.net.nz/thymeleaf/layout"
      layout:decorate="~{layout/main}">
<head>
</head>
<body>
    <div layout:fragment="content">
        <!-- indexページ専用のコンテンツをここに配置 -->
        <h1>Welcome to Anime World!</h1>
        <p>Explore the latest and most popular anime collections right here.</p>
    </div>
</body>
</html>
```

このindex.htmlでは、layout:decorateでlayout/main.htmlを親テンプレートとして指定し、layout:fragment="content"の中に子ページの内容を記述しています。これにより、layout/main.htmlの共通レイアウトが適用され、ページごとに異なる内容を挿入できます。

詳細なFragmentの使い方

Thymeleafのlayout:fragmentを使うと、複数の部分テンプレートを効率的に管理し、異なるページで再利用できます。以下に、よく使われるfragmentの例を紹介します。

## 1. 複数のFragmentを設定する

layout/main.htmlで複数のlayout:fragmentを定義することで、個別のページで柔軟に異なる部分を設定できます。

```
<header layout:fragment="header">
    <!-- ヘッダーの内容 -->
</header>

<main layout:fragment="content">
    <!-- メインコンテンツ -->
</main>

<footer layout:fragment="footer">
    <!-- フッターの内容 -->
</footer>
```

## 2. 個別ページでのFragment指定

index.htmlのような子ページで、これらのFragmentをそれぞれ指定することで、必要な部分だけを挿入できます。

```
<div layout:fragment="header">
    <h1>Custom Header Content</h1>
</div>

<div layout:fragment="content">
    <h2>Index Page Content</h2>
    <p>This is specific content for the index page.</p>
</div>

<div layout:fragment="footer">
    <p>Custom footer text for index page</p>
</div>
```

## 3. Fragmentをインクルードする

別のテンプレートから特定のFragmentを呼び出してインクルードすることも可能です。

```
<div th:insert="~{layout/main :: header}"></div>
```

## Conclusion

Thymeleaf Layout Dialectのlayout:fragmentを活用すると、Spring Bootアプリケーションで一貫性のあるテンプレート管理が可能になり、各ページに柔軟なカスタムコンテンツを追加できます。この方法により、コードの重複を最小限に抑えつつ、メンテナンス性を向上させることができます。
