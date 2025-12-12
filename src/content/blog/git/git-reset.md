---
author: Taro Gray
pubDatetime: 2025-11-30T22:30:00Z
title: how to reverse to the previous state before committing
postSlug: git-reset
featured: true
draft: false
tags:
  - git
description: git reset coomand
---

## Table of contents

`git reset` は **「コミットの履歴を戻したり、ステージング状態を戻したりするコマンド」** です。
用途によって動きが全然違うので、まずは **どのタイプを使うか** を理解するのが大事です。

---

## ✅ 1. `git reset` の3つの種類（超重要）

## **1) `--soft`**

### コミットだけ取り消したい（ファイル内容はそのまま）

```
git reset --soft HEAD~1
```

- 直前のコミットを取り消す
- 変更内容はステージングされた状態で残る (`git add` 済みの状態)
- コミットメッセージを変えたいときに便利

---

## **2) `--mixed`（デフォルト）**

### コミットとステージングを取り消したい（ファイル内容はそのまま）

```
git reset HEAD~1
```

or

```
git reset --mixed HEAD~1
```

- 直前のコミットを取り消す
- 変更内容は「ワークツリー」には残るけど **ステージングから外れる**
- コードは残したまま、add をやり直したいときに使う

---

## **3) `--hard`（危険）**

### 全部なかったことにしたい（ファイルも消える）

```
git reset --hard HEAD~1
```

- コミットも履歴も
- **ファイルの実際の変更も全部消える**
- 元に戻せない（普通は）

※ これはミスると地獄なので慎重に使う。

---

## ✅ 2. よく使うパターン

### ● コミットを1つ戻したい（変更は残す）

```
git reset --mixed HEAD~1
```

---

## ● コミットを取り消してやり直したい（変更も消す）

```
git reset --hard HEAD~1
```

---

## ● あるファイルをステージングから外したい（add を取り消す）

```
git reset HEAD <file>
```

例：

```
git reset HEAD src/newfile.md
```

---

## ✅ 3. 今のあなたの状況に一番関係あるのはどれ？

あなたの問題は：

> 新規ディレクトリだけ Git が認識してて、中のファイルが認識されない
> → add / commit の状態がおかしい

その場合によく使うのは **ステージングをクリアしたい** パターン。

### 👉 全部の staging を取り消してリセット

```
git reset
```

これだけで **ステージング解除（mixed reset）** されます。

そのあとあらためて：

```
git add newdir -A
git status
```

とやれば、**中のファイルも含めて全部ちゃんと見えるはず**。

---
