---
author: Taro Gray
pubDatetime: 2024-02-18T15:02:00Z
title: Thymeleafの魔法：th:fieldを使ってフォームを動的に扱う
postSlug: thymeleaf-th-field
featured: true
draft: false
tags:
  - Thymeleaf
  - th-field
description: th:fieldを使うことで、フォームのハンドリングが格段に楽になり、エラーハンドリングやデータの再表示がスムーズに行えるようになります。ThymeleafとSpring Bootを活用して、より良い
---

## Table of contents

Spring BootとThymeleafを組み合わせることで、動的なWebアプリケーションを容易に構築できます。特に、フォームのデータバインディングには`th:field`が非常に有効です。このブログでは、`th:field`の使い方とその魅力について、中級者向けに解説します。

## th:fieldとは？

`th:field`はThymeleafの属性で、フォームのフィールドとコントローラーのモデル属性をバインディングするために使用されます。これにより、フォームの入力値をサーバーに送信する際に、手動で各フィールドをマッピングする手間を省き、エラーメッセージの表示やフィールド値の保持が容易になります。

## 具体例：ユーザー登録フォーム

ユーザー情報を入力するフォームをThymeleafで作成する例を見てみましょう。

### モデルクラス

まず、フォームのデータを保持するためのモデルクラス`User`を作成します。

```java
public class User {
    private String name;
    private String email;
    // getterとsetter
}
```

### コントローラー

次に、モデルをフォームにバインディングするためのコントローラーを作成します。

```java
@Controller
public class UserController {

    @GetMapping("/register")
    public String showForm(Model model) {
        model.addAttribute("user", new User());
        return "register";
    }

    @PostMapping("/register")
    public String submitForm(@ModelAttribute User user) {
        // ユーザー登録処理
        return "registerSuccess";
    }
}
```

### Thymeleafテンプレート

`th:field`を使用して、モデル属性をフォームフィールドにバインディングします。

```html
<!doctype html>
<html xmlns:th="http://www.thymeleaf.org">
  <head>
    <title>ユーザー登録</title>
  </head>
  <body>
    <form action="#" th:action="@{/register}" th:object="${user}" method="post">
      <label for="name">名前:</label>
      <input type="text" th:field="*{name}" />

      <label for="email">メールアドレス:</label>
      <input type="email" th:field="*{email}" />

      <button type="submit">登録</button>
    </form>
  </body>
</html>
```

この例では、`th:object="${user}"`でフォームにモデルを指定し、`th:field="*{name}"`でモデルの`name`プロパティを`<input>`タグにバインディングしています。これにより、フォームの入力値が`User`オブジェクトのプロパティに自動的にマッピングされます。

## リンクと参考文献

- [Thymeleaf + Spring Documentation](https://www.thymeleaf.org/doc/tutorials/3.0/thymeleafspring.html) - ThymeleafとSpringの統合に関する公式ドキュメント。
- [Baeldung on Thymeleaf](https://www.baeldung.com/thymeleaf-in-spring-mvc) - Thymeleafの基本的な使い方に関する詳細なガイド。
