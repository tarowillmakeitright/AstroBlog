---
author: Taro Gray
pubDatetime: 2024-10-08T08:00:00.00Z
title: Dockerコマンド解説: 効率的なコンテナ管理のための基本操作
postSlug: docker-command-explanation-for-efficient-container-management
featured: true
draft: false
tags:
  - docker create
  - docker pull 
  - docker start
  - docker ps
  - docker run
  - docker rm
  - docker image rm
  - docker image ls
description: Dockerを使ってコンテナやイメージを管理するための基本コマンドについて解説します。それぞれのコマンドの使い方と、どういった場面で使うべきかを詳しく紹介します。
---

## Table of contents

    1.	Docker create
    2.	Docker pull
    3.	Docker start
    4.	Docker ps
    5.	Docker run
    6.	Docker rm
    7.	Docker image rm
    8.	Docker image ls
    9.	Docker network create
    10.	Apache, MySQL, OpenJDKの使用例
    11.	DockerでMySQLコンテナの詳細な設定

## 1. Docker create

docker create イメージ名

説明: このコマンドは、Dockerコンテナを作成しますが、すぐには起動しません。コンテナを作成し、その設定を保存したい場合に使用されます。起動をせずにコンテナを作成しておくことで、あとで必要なときに素早く起動できます。

## 2. Docker pull

docker pull イメージ名

説明: Docker Hubなどのリポジトリからイメージをダウンロードするコマンドです。コンテナを起動するためにはまずイメージが必要なので、事前にイメージを取得します。

使用例: docker pull mysql:latest は、最新バージョンのMySQLイメージをDocker Hubからプルします。

## 3. Docker start

docker start コンテナ名

説明: 既に作成されたコンテナを起動するコマンドです。docker createで作成されたが、まだ起動していないコンテナを動かすために使います。

## 4. Docker ps

docker ps

説明: 現在実行中のコンテナの一覧を表示します。-aオプションを付けると、停止したコンテナも含めて表示できます。

## 5. Docker run

docker run --name コンテナ名 -d -p 8080:80 イメージ名

説明: コンテナを作成して、同時に実行します。--nameでコンテナ名を指定し、-dでデタッチモード（バックグラウンド実行）、-pでホストのポートとコンテナのポートをマッピングします。この例では、ホストのポート8080をコンテナのポート80にマッピングし、バックグラウンドでApacheなどのWebサーバを動かすことができます。

## 6. Docker rm

docker rm コンテナ名

説明: 停止したコンテナを削除します。不要になったコンテナを削除してディスクスペースを確保するために使用します。

## 7. Docker image rm

docker image rm イメージ名

説明: Dockerイメージを削除します。もう使わないイメージや、ディスクスペースを節約したいときに有効です。

## 8. Docker image ls

docker image ls

説明: ローカルに保存されているすべてのDockerイメージを表示します。どのイメージがローカルにあるかを確認するときに使用します。

## 9. Docker network create

docker network create ネットワーク名

説明: 新しいDockerネットワークを作成します。ネットワークを作成することで、コンテナ同士を独立したネットワーク上で通信させることが可能です。これにより、セキュリティを強化したり、複数のコンテナが効率よく通信できるようになります。

なぜ使うのか: コンテナ同士を特定のネットワーク内で安全に通信させたい場合や、サービス間の接続を確立するために使います。

## 10. Apache, MySQL, OpenJDKの使用例

Apacheのイメージ

docker pull httpd:latest

Apache HTTP Serverのイメージをプルして、WebサーバーをDockerで簡単に起動できます。

MySQLのイメージ

docker pull mysql:latest

MySQLのイメージをプルして、データベースサーバーを簡単にセットアップできます。

OpenJDKのイメージ

docker pull openjdk:17

Java開発用のOpenJDKイメージをプルして、Javaアプリケーションを実行できます。

## 11. DockerでMySQLコンテナの詳細な設定

以下のコマンドは、MySQLコンテナをより詳細に設定して起動する例です。ネットワーク名や環境変数を指定して、データベースの初期設定を行います。

docker run --name my-mysql-container -dit --net=my-network \
 -e MYSQL_ROOT_PASSWORD=password \
 -e MYSQL_DATABASE=my-database \
 -e MYSQL_USER=my-user \
 -e MYSQL_PASSWORD=my-password \
 mysql --character-set-server=utf8mb4 --collation-server=utf8mb4_general_ci --default-authentication-plugin=mysql_native_password

説明:

    •	–net=my-network: 事前に作成したカスタムネットワークを指定して、同じネットワーク内でコンテナ同士を通信できるようにします。
    •	-e オプション: 環境変数を設定し、MySQLの初期設定を行います（ルートパスワード、データベース名、ユーザー名、パスワードなど）。
    •	MySQLオプション: --character-set-server=utf8mb4 や --collation-server=utf8mb4_general_ciなどで文字セットや照合順序を指定しています。また、--default-authentication-plugin=mysql_native_passwordで認証方式も設定します。

## まとめ

このブログでは、Dockerでの基本的なコンテナ管理コマンドを解説しました。それぞれのコマンドは、効率的なコンテナの作成、管理、削除に役立ちます。特に、ネットワークの作成や複数のコンテナの連携には、ネットワーク設定が重要です。
