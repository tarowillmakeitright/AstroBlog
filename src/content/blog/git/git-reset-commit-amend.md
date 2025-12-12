---
author: Taro Gray
pubDatetime: 2023-11-24T12:46:00Z
title: Gitのタイムマシン操作 `git reset` と `git commit --amend`
postSlug: git-reset-commit-amend
featured: true
draft: false
tags:
  - GitHub
  - git reset
  - git commit amend
description: git reset と git commit --amend は、あなたのGit履歴を管理するための強力なツールです。これらのコマンドを適切に使用することで、プロジェクトの履歴をクリーンで、追跡しやすいものに保つことができます。ただし、これらのコマンドは特に `reset --hard` のように強力なため、使用する際には十分な注意が必要です。正しく使えば、あなたのGit履歴はいつでもクリーンで整理された状
---

## Table of contents

Gitは単なるバージョン管理システムではありません。それは過去を書き換え、未来を再定義するタイムマシンのようなものです。このブログでは、`git reset` と `git commit --amend` の2つの強力なコマンドを中級者向けに掘り下げます。これらのコマンドを使いこなすことで、あなたのコミット履歴をよりクリーンで理解しやすいものにすることができます。

## `git reset` の探検

### 基本的な使用法

`git reset` コマンドは、現在のブランチのHEADを指定した状態にリセットします。これには3つの主要なオプションがあります：`--soft`, `--mixed`（デフォルト）、`--hard`。

```bash
git reset --hard <コミットハッシュ>
```

### 面白い例: コミットのゴミ箱

想像してみてください。あなたが過去のコミットを「ゴミ箱」に捨てることができるとしたら？例えば、最新のコミットがまったくの失敗作だと気付いたら、以下のコマンドでそのコミットを「消去」できます。

```bash
git reset --hard HEAD~1
```

これで、最新のコミットがなかったことにできます。ただし、使用する際は注意が必要です。`--hard` オプションは元に戻せない変更を加えるため、失われた変更を取り戻すことはできません。

## `git commit --amend` の魔法

### 基本的な使用法

`git commit --amend` コマンドは、最新のコミットを修正するために使用されます。これは、コミットメッセージの編集や、ステージングされた変更の追加に便利です。

```bash
git commit --amend -m "新しいコミットメッセージ"
```

### 面白い例: コミットメッセージの時間旅行

あなたが過去に戻って、コミットメッセージを「修正」することができるとしたら？`git commit --amend` コマンドを使えば、まるでタイムトラベラーのように最新のコミットメッセージを修正できます。

例えば、タイポを修正したい場合は、`--amend` オプションを使用して新しいメッセージを追加します。これは、小さなミスを修正するのに非常に便利です。

## 参考リンク

- [Git Reset Documentation](https://git-scm.com/docs/git-reset)
- [Git Commit --amend Documentation](https://git-scm.com/docs/git-commit#Documentation/git-commit.txt---amend)
