---
author: Taro Gray
pubDatetime: 2024-11-10T10:00:00.00Z
title: Spring Bootで.envファイルを使ったMongoDB接続設定
postSlug: spring-boot-env-mongodb-connection
featured: true
draft: false
ogImage: (任意のURLを設定)
tags:
  - MongoPassword
  - .env
  - application.properties
  - Spring Boot
description: .envファイルからMongoDBの接続URIを読み込み、Spring Bootのapplication.propertiesで受け渡す方法を解説します。環境変数の設定で接続情報を管理し、より安全で柔軟なアプリケーション構成を実現します。
---

## Table of Contents

## Introduction

Spring BootでMongoDBに接続する際、環境変数（.envファイル）から接続URIを取得する方法を解説します。この設定により、アプリケーションの構成ファイルに機密情報を直接記載することなく、柔軟な環境構築が可能です。環境変数を使った設定は、特に本番環境でのセキュリティ向上に役立ちます。

## 環境変数としてMongoDB URIを設定

まず、プロジェクトのルートディレクトリに.envファイルを作成します。このファイルにMongoDBの接続URIを環境変数として記載します。

.envファイルの内容

.envファイルには、以下のようにMongoDBのURIを設定します：

MONGODB_URI=mongodb+srv://userName:password@ClusterName/dbName?retryWrites=true&w=majority&appName=Cluster0

    •	userName: MongoDBのユーザー名
    •	password: MongoDBのパスワード
    •	ClusterName: MongoDBクラスタの名称
    •	dbName: データベース名

環境変数で機密情報を管理することで、セキュリティと柔軟性を向上させることができます。

## application.propertiesでの受け渡し

次に、Spring Bootのapplication.propertiesファイルで、.envファイルの内容を使ってMongoDBに接続する設定を行います。Spring Bootは、application.propertiesからMongoDBのURIを読み込むことで、MongoDBサーバーに接続します。

spring.data.mongodb.uri=${MONGODB_URI}

この設定により、application.propertiesはMONGODB_URIという環境変数からMongoDBのURIを取得します。これにより、ソースコードやプロジェクト内で直接接続情報を記述することなく、MongoDBに接続できます。

Spring Bootでの.envファイルの読み込み設定

.envファイルを読み込むためには、spring-boot-starter-dotenvなどのライブラリを導入すると、.envファイルの内容を環境変数として扱うことが容易になります。あるいは、System.getenv()を使って、Javaコード内で直接読み込むことも可能です。

## まとめ

環境変数を利用したMongoDB接続の設定は、アプリケーションのセキュリティと柔軟性を大幅に向上させます。特に、application.propertiesでの環境変数利用によって、異なる環境（開発・本番）で異なる接続設定を簡単に切り替えることが可能です。
