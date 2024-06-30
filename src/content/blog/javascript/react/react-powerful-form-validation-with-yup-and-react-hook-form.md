---
author: Taro Gray
pubDatetime: 2024-06-30T15:51:00.00Z
title: YupとReact Hook Formで強力なフォームバリデーションを実現
postSlug: react-powerful-form-validation-with-yup-and-react-hook-form
featured: true
draft: false
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - JavaScript
  - React
  - React Hook Form
  - Yup
description: YupとReact Hook Formを組み合わせて、効果的なフォームバリデーションを簡単に実装する方法を解説します。この組み合わせにより、開発者はフォームデータの検証をより簡潔に、効率的に行うことができます。
---

## 目次

## YupとReact Hook Formの組み合わせ

React Hook Formはフォームの状態管理を簡素化し、Yupは強力なスキーマベースのバリデーションを提供します。この二つを組み合わせることで、フォームの検証ロジックを外部のスキーマに委ねることができ、コードの保守性と可読性が向上します。

## 基本的なフォームの設定とバリデーション

以下のコードスニペットは、Yupを使用してフォーム入力のバリデーションルールを設定し、React Hook Formでこれを利用する方法を示しています。

```jsx
import { useForm } from "react-hook-form";
import { yupResolver } from "@hookform/resolvers/yup";
import * as yup from "yup";

// バリデーションルールを定義
const schema = yup
  .object({
    name: yup
      .string()
      .required("名前は必須入力です。")
      .max(20, "名前は最大20文字までです。"),
    gender: yup.string().required("性別は必須入力です。"),
  })
  .required();

export default function FormYup() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm({
    resolver: yupResolver(schema),
  });

  const onSubmit = data => console.log(data);
  const onError = errors => console.log(errors);

  return (
    <form onSubmit={handleSubmit(onSubmit, onError)}>
      <label htmlFor="name">名前:</label>
      <input id="name" type="text" {...register("name")} />
      <p>{errors.name?.message}</p>
      <label>性別:</label>
      <input type="radio" value="male" {...register("gender")} /> 男性
      <input type="radio" value="female" {...register("gender")} /> 女性
      <p>{errors.gender?.message}</p>
      <button type="submit">送信</button>
    </form>
  );
}
```

このコードでは、`yupResolver`を使ってYupのバリデーションルールをReact Hook Formに統合しています。`register`メソッドを使用して各入力フィールドをフォームに登録し、`handleSubmit`でバリデーションを行います。

## 参考文献

- [React Hook Form - Get Started](https://react-hook-form.com/get-started)
- [Yup - API Documentation](https://github.com/jquense/yup)

## まとめ

YupとReact Hook Formを組み合わせることで、Reactアプリケーションにおけるフォームのバリデーションが非常にシンプルかつ効果的に行えます。これにより、開発者はフォーム処理のコードを
