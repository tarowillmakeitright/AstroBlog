---
author: Taro Gray
pubDatetime: 2024-10-10T00:00:00.00Z
title: Dockerでのコンテナイメージ化とイメージ管理の基本
postSlug: creating-and-managing-docker-images
featured: true
draft: false
tags:
  - docker commit
  - docker build
  - docker save
description: Dockerでコンテナのイメージ化やDockerfileを使ったイメージ作成方法、そしてイメージの保存について詳しく解説します。各コマンドの使い方と、どのような場面で使用するべきかを理解しましょう。
---

## Table of contents

## 1. Docker commit: コンテナをイメージ化する

docker commit コンテナ名 作成するイメージ名

説明: 既に動作中、または停止中のコンテナから新しいイメージを作成するコマンドです。このコマンドを使用すると、コンテナで実行した変更をそのまま保存し、再利用できるイメージを作成できます。

なぜ使うのか？
Docker commitは、開発や設定変更を行ったコンテナの状態をそのまま新しいイメージとして保存したいときに使います。例えば、あるコンテナに対してソフトウェアのインストールや設定を行った後、その状態を保持したイメージを作成し、他の環境で再利用することが可能です。

## 2. Docker build: Dockerfileを使ったイメージ作成

docker build -t 作成するイメージ名 材料フォルダのパス

説明: Dockerfileを使用して、新しいDockerイメージをビルドするコマンドです。-tオプションでイメージに名前を付け、材料フォルダのパスでDockerfileがあるディレクトリを指定します。

なぜ使うのか？
Docker buildは、コードベースや設定を持つ環境を標準化したイメージを作成するために使います。Dockerfileに一連の手順を定義することで、イメージを再現性高く作成でき、開発環境と本番環境の違いを最小限に抑えることができます。

## 3. Dockerfileの主要コマンド

Dockerfileを使ってイメージを作成する際に、いくつかの主要なコマンドがあります。それぞれの役割を理解することが重要です。

Dockerfileのコマンド例と説明

    1.	FROM:

ベースイメージを指定します。イメージのビルドは、このベースイメージから始まります。

FROM ubuntu:20.04

    2.	ADD / COPY:

ホストマシンのファイルやディレクトリをコンテナ内にコピーします。

COPY ./app /usr/src/app

    3.	RUN:

イメージのビルド中に実行するコマンドを指定します。ソフトウェアのインストールなどに使用されます。

RUN apt-get update && apt-get install -y nginx

    4.	CMD / ENTRYPOINT:

コンテナ起動時に実行されるデフォルトのコマンドを指定します。CMDは上書き可能、ENTRYPOINTは固定されます。

CMD ["nginx", "-g", "daemon off;"]

    5.	EXPOSE:

コンテナが使用するポートを指定します。

EXPOSE 80

    6.	VOLUME:

ボリュームを指定して、コンテナ内で永続的にデータを保存します。

VOLUME /data

    7.	ENV:

環境変数を設定します。

ENV APP_ENV=production

    8.	WORKDIR:

コンテナ内での作業ディレクトリを指定します。

WORKDIR /usr/src/app

    9.	LABEL:

イメージにメタデータを付与します。バージョン情報や開発者情報を含めることができます。

LABEL maintainer="taro@example.com"

    10.	ARG:

ビルド時に使用する引数を定義します。ENVと異なり、ビルド時にのみ使用されます。

ARG VERSION=1.0.0

    11.	HEALTHCHECK:

コンテナの状態をチェックするためのヘルスチェックコマンドを定義します。

    1.	FROM: ベースイメージを指定します。イメージのビルドは、このベースイメージから始まります。

FROM ubuntu:20.04

    2.	ADD / COPY: ホストマシンのファイルやディレクトリをコンテナ内にコピーします。

COPY ./app /usr/src/app

    3.	RUN: イメージのビルド中に実行するコマンドを指定します。ソフトウェアのインストールなどに使用されます。

RUN apt-get update && apt-get install -y nginx

    4.	CMD / ENTRYPOINT: コンテナ起動時に実行されるデフォルトのコマンドを指定します。CMDは上書き可能、ENTRYPOINTは固定されます。

CMD ["nginx", "-g", "daemon off;"]

    5.	EXPOSE: コンテナが使用するポートを指定します。

EXPOSE 80

    6.	VOLUME: ボリュームを指定して、コンテナ内で永続的にデータを保存します。

VOLUME /data

    7.	ENV: 環境変数を設定します。

ENV APP_ENV=production

    8.	WORKDIR: コンテナ内での作業ディレクトリを指定します。

WORKDIR /usr/src/app

    9.	LABEL: イメージにメタデータを付与します。バージョン情報や開発者情報を含めることができます。

LABEL maintainer="taro@example.com"

    10.	ARG: ビルド時に使用する引数を定義します。ENVと異なり、ビルド時にのみ使用されます。

ARG VERSION=1.0.0

    11.	HEALTHCHECK: コンテナの状態をチェックするためのヘルスチェックコマンドを定義します。

HEALTHCHECK CMD curl --fail http://localhost:80 || exit 1

なぜ使うのか？
Dockerfileは、イメージ作成の手順を明確にし、簡単に再現可能なビルドプロセスを提供します。これにより、複雑なセットアップ手順を簡単に自動化し、チーム全体で共有できます。

## 4. Docker save: イメージの保存

docker save -o ファイル名.tar イメージ名

説明: Dockerイメージを.tarファイルとして保存するコマンドです。保存されたイメージは、他の環境に持ち込んだり、他のユーザーと共有したりすることができます。

なぜ使うのか？

Docker saveは、ローカルでビルドしたイメージをバックアップしたり、別のサーバーや環境に持ち込む場合に使用します。例えば、インターネットに接続されていない環境でイメージを配布する必要がある場合、.tarファイルとして保存しておくと便利です。

## 5. まとめ

このブログでは、Dockerにおけるコンテナのイメージ化やDockerfileを使ったイメージ作成、そして作成したイメージを保存する方法について解説しました。

    •	Docker commitは、コンテナの現在の状態を新しいイメージとして保存するために使います。
    •	Docker buildは、Dockerfileを使って再現可能なイメージを作成するために使用します。
    •	Docker saveは、イメージをバックアップしたり他の環境に移行する際に役立ちます。

これらのコマンドを適切に活用することで、Dockerを使用した開発やデプロイのプロセスをより効率的に進めることが可能です。
