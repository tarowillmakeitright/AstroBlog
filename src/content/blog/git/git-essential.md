---
author: Taro Gray
pubDatetime: 2024-04-30T22:30:00Z
title: Gitコマンドまとめ
postSlug: git-essential
featured: true
draft: false
tags:
  - clone
  - branch
  - branch model
  - git-flowモデル
  - add
  - push
  - status
  - merge
  - rebase
  - statsh
  - tag
description: Gitをそこそこ使いこなすために必要な基礎知識やコマンドをまとめました。
---

## Table of contents

## Gitとは

分散型バージョン管理システムです。今時のソースコード管理にはほぼ必ずGitが使用されます。GitHub、GitLab、GitBucket、BitBucketなど複数のサービスがありますが、使用するサービスはチーム事情や会社事情によって決まります。

## clone

リモートリポジトリをローカルにダウンロードするコマンドです。

```bash
git clone <URL>
```

## ブランチ

ブランチは作業履歴を枝分かれさせて記録します。ブランチ上での変更は他のブランチには影響しません。

## ブランチモデル

ブランチの運用方法には様々なモデルがありますが、git-flowとGitHub Flowが特に有名です。

## git-flowモデル

- **masterブランチ**: リリース可能な品質を保証するブランチ。
- **developブランチ**: 開発の主軸となるブランチ。
- **featureブランチ**: 新機能の開発やバグ修正を行うブランチ。
- **releaseブランチ**: リリース前の最終調整を行うブランチ。
- **hotfixブランチ**: リリース後の緊急修正を行うブランチ。
- **supportブランチ**: 旧バージョンのサポートを行うブランチ。

## GitHub Flowモデル

- **masterブランチ**: すべての機能がマージされる主ブランチ。
- **topicブランチ**: 任意のトピックごとに作成されるブランチ。

## リモートリポジトリとbranchの違い

- **リモートリポジトリ**: チーム間で共有されるコードの中央集権的な保管場所。
- **ブランチ**: 単一のリポジトリ内で異なる開発タスクを同時に進行する手段。

## その他の重要なGitコマンド

## status

変更されたファイルを表示します。

```bash
git status
```

## add

変更をステージング環境に追加します。

```bash
git add <file>
```

## commit

変更をリポジトリにコミットします。

```bash
git commit -m "コミットメッセージ"
```

## push

ローカルの変更をリモートリポジトリにプッシュします。

```bash
git push origin <branch>
```

## pull

リモートリポジトリから最新の変更を取得し、ローカルリポジトリにマージします。

```bash
git pull
```

## merge

異なるブランチの変更を現在のブランチに統合します。

```bash
git merge <branch>
```

## rebase

ブランチの変更を別のブランチの上に再適用します。

```bash
git rebase <branch>
```

## stash

未コミットの変更を一時保存します。

```bash
git stash
git stash pop
```

## tag

重要なポイントにタグをつけます。

```bash
git tag <tagname>
git push origin <tagname>
```

## 関連記事

- [Git documentation](https://qiita.com/jesus_isao/items/63557eba36819faa4ad9) - Git周り（レポジトリ、コミット、ローカル、VSコード、タグ、ブランチ）説明書
- [Essntial Git Command ](https://qiita.com/gold-kou/items/7f6a3b46e2781b0dd4a0#%E3%83%96%E3%83%A9%E3%83%B3%E3%83%81%E4%BD%9C%E6%88%90) - Git コマンドの使えるWebサイト。
