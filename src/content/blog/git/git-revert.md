---
author: Taro Gray
pubDatetime: 2025-11-30T22:34:00.000Z
title: Gitでの変更を元に戻す方法
postSlug: git-reset-restore-revert
featured: true
tags:
  - git
description: how to restore the previous state
---

## Table of Contents

取り消したい内容によって使う Git コマンドが違います。
**「何を取り消したいのか」ごとにまとめた表が一番覚えやすいです。**

---

## ✅ Git の“取り消し”コマンド一覧（これ覚えれば完璧）

## **1. `git restore`**

### ✔ ファイルの変更を消したい（作業ディレクトリの変更を取り消す）

```
git restore <file>
```

### ✔ `git add` したのを取り消したい（ステージング解除）

```
git restore --staged <file>
```

👉 **安全**で、最近の Git はこれ推奨。

---

## **2. `git reset`**

### ✔ ステージング解除（`git add` をなかったことに）

```
git reset <file>
```

### ✔ コミットを取り消す（変更内容は残す）

```
git reset HEAD~1
```

（= `--mixed`）

### ✔ 全部を完全に取り消す（危険！）

```
git reset --hard HEAD~1
```

---

## **3. `git revert`**

### ✔ 公開済みコミットを「取り消しコミット」で相殺したい（履歴は消さない）

```
git revert <commit-id>
```

👉 チーム作業 / push 済みで安全に巻き戻したい時はこれ一択。

---

今は `git restore` と `git switch` に分離。

---

## 🔥 ケース別「取り消し早見表」

| やりたいこと                           | 使うコマンド                  |
| -------------------------------------- | ----------------------------- |
| ローカルの編集を消したい               | `git restore <file>`          |
| add を取り消したい                     | `git restore --staged <file>` |
| 最後のコミットを消したい（変更は残す） | `git reset HEAD~1`            |
| 最後のコミットを完全に消したい         | `git reset --hard HEAD~1`     |
| push 済みのコミットを取り消したい      | `git revert <commit-id>`      |
| 新しいブランチに移動したい             | `git switch <branch>`         |

---

## 🚀 たぶん今のあなたが使うのはこれ

### **ステージング全部クリア**

```
git reset
```

または

```
git restore --staged .
```

### **ファイルの変更を取り消す**

```
git restore .
```
