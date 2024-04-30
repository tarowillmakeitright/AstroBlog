---
author: Taro Gray
pubDatetime: 2024-02-04T14:47:00.000Z
title: Spring Bootのキャッシング戦略：@Cacheable, @CacheEvict, @Caching
postSlug: springBoot-cacheable-casheevict-caching
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - Java
  - Spring Boot
description: Cacheable, @CacheEvict, そして@Cachingは、Spring Bootアプリケーションのパフォーマンスを向上させるための強力なツールです。これらのアノテーションを適切に使用することで、アプリケーションのレスポンス時間を短縮し、バックエンドの負荷を軽減することができます。キャッシュ戦略を計画的に実装して、あなたのアプリケーションを次のレベルに引き上げましょう！
---

## Table of contents

Spring Bootでのキャッシングは、アプリケーションのパフォーマンスを大幅に向上させる魔法のような手段です。このブログでは、Spring Bootのキャッシングメカニズムである`@Cacheable`, `@CacheEvict`, そして`@Caching`アノテーションの使い方を探検します。それでは、中級者向けの具体例を交えながら、この冒険を始めましょう。

## 1. @Cacheable

`@Cacheable`アノテーションは、メソッドの戻り値をキャッシュに保存することで、同じ引数での次回の呼び出しを高速化します。

### コード例：ユーザー情報のキャッシュ

```java
@Service
public class UserService {

    @Cacheable("users")
    public User findUserById(Long id) {
        // データベースからユーザーを検索する重い処理を想定
        return userRepository.findById(id).orElse(null);
    }
}
```

この例では、`findUserById`メソッドの結果は、"users"という名前のキャッシュに保存されます。同じ`id`でメソッドが再び呼び出された場合、結果はキャッシュから直接取得され、データベースへのアクセスは発生しません。

## 2. @CacheEvict

`@CacheEvict`アノテーションは、条件に一致するキャッシュを削除します。これにより、データの整合性を保ちながらキャッシュの利点を享受できます。

### コード例：ユーザー情報のキャッシュ削除

```java
@Service
public class UserService {

    @CacheEvict(value = "users", key = "#id")
    public void deleteUserById(Long id) {
        // ユーザーの削除処理
        userRepository.deleteById(id);
    }
}
```

この例では、`deleteUserById`メソッドが呼び出されると、指定された`id`を持つ"users"キャッシュのエントリが削除されます。

## 3. @Caching

`@Caching`アノテーションは、複数のキャッシング操作（`@Cacheable`, `@CacheEvict`など）を一つのメソッドに適用する場合に使用します。

### コード例：複合キャッシング操作

```java
@Service
public class UserService {

    @Caching(evict = {
        @CacheEvict(value = "users", key = "#id"),
        @CacheEvict(value = "userDetails", allEntries = true)
    })
    public void updateUser(User user) {
        // ユーザーの更新処理
        userRepository.save(user);
    }
}
```

この例では、`updateUser`メソッドが実行されると、特定のユーザーに関連するキャッシュと、"userDetails"キャッシュ内のすべてのエントリが削除されます。

## リンクと参考文献

- [Spring Boot Caching Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/io.html#io.caching) - Spring Bootの公式キャッシングドキュメント。
- [Baeldung on Spring Cache](https://www.baeldung.com/spring-cache-tutorial) - Spring Cacheに関する包括的なガイド。
