---
author: Taro Gray
pubDatetime: 2024-01-21T00:27:00.000Z
title: RESTful API操作のガイド：`curl`と`httpie`を使って
postSlug: linux-restfulAPI-test
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Linux
description: このブログでは、`curl`と`httpie`を使ってAPIとやりとりする基本的な方法を解説しました。特に`httpie`を使ったPOSTリクエストの作成方法に焦点を当て、JSON形式でのデータ送信方法を明確にしました。これらのツールは、APIエンドポイントのテストやデバッグに非常に役立ちます。
---

## Table of contents

RESTful APIとのやりとりは、開発者にとって日常的な作業です。このブログでは、ターミナルから`curl`と`httpie`を使って、様々なHTTPメソッド（POST, GET, PUT, DELETE）をテストする方法を解説します。特に`httpie`の`key1=value1`のようなデータの送信方法に焦点を当てます。

## `curl`を使用したAPI操作

`curl`は多くのUnix系システム（macOS、Linuxなど）で利用可能なコマンドラインツールです。

### GET

データをサーバーから取得します。

```bash
curl http://example.com/api/resource
```

### POST

サーバーに新しいリソースを作成するためのデータを送信します。

```bash
curl -X POST -H "Content-Type: application/json" -d '{"key1":"value1", "key2":"value2"}' http://example.com/api/resource
```

### PUT

サーバー上のリソースを更新します。

```bash
curl -X PUT -H "Content-Type: application/json" -d '{"key1":"newvalue1", "key2":"newvalue2"}' http://example.com/api/resource/1
```

### DELETE

サーバー上のリソースを削除します。

```bash
curl -X DELETE http://example.com/api/resource/1
```

## `httpie`を使用したAPI操作

`httpie`は、より直感的なコマンドラインHTTPクライアントです。

### GET

```bash
http GET http://example.com/api/resource
```

### POST

```bash
http POST http://example.com/api/resource key1=value1 key2=value2
```

### PUT

```bash
http PUT http://example.com/api/resource/1 key1=newvalue1 key2=newvalue2
```

### DELETE

```bash
http DELETE http://example.com/api/resource/1
```

`httpie`は、`key1=value1`の形式でデータを送信する際、JSONオブジェクトに変換して送ります。これはAPIがJSON形式のデータを期待している場合に非常に便利です。

## `httpie`での`key1=value1`

`key1=value1`では、`key1`は送信するフィールドまたはパラメータの名前、`value1`はその値を示します。`httpie`を使用すると、このキーと値のペアがHTTPリクエストの本文に送信されます。

```bash
http POST http://example.com/api/resource key1=value1 key2=value2
```

上記のコマンドは、以下のJSON本文を`http://example.com/api/resource`に送信します。

```json
{
  "key1": "value1",
  "key2": "value2"
}
```

これにより、`key1`と`key2`というフィールドがそれぞれ`value1`と`value2`という値を持つJSONオブジェクトが作成されます。

## 参考文献

- `curl`と`httpie`に関する詳細は、それぞれの公式ドキュメントを参照してください。
  - [curl documentation](https://curl.se/docs/)
  - [httpie documentation](https://httpie.io/docs)
