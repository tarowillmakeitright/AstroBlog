---
author: Taro Gray
pubDatetime: 2024-01-07T13:50:00.00Z
title:  Git の新星 `git switch` コマンドの探求
postSlug: git-switch
featured: true
draft: false
tags:
  - Git
  - git switch
description: `git switch` は、Git の使い勝手を向上させる素晴らしいコマンドです。このコマンドを使いこなし、より効率的にブランチを操作しましょう！
---

## Table of contents

Git 2.23で導入された `git switch` コマンドは、ブランチ操作のための新しい、より直感的な方法を提供します。従来の`git checkout`の機能を分割し、特にブランチの切り替えに関する操作を明確化しています。この記事では、`git switch` の使い方とその魅力を中級者向けに解説します。

## `git switch` の基本

`git switch` コマンドは、ローカルブランチ間で切り替えるために使用します。基本的な使用法は以下の通りです:

```bash
git switch <ブランチ名>
```

この単純なコマンドで、指定したブランチに素早くスイッチできます。

## 新しいブランチへのスイッチ

新しいブランチを作成し、そのブランチに切り替える場合は `-c` オプションを使用します。以下はその例です:

```bash
git switch -c new-branch
```

これは `new-branch` という新しいブランチを作成し、そこに切り替えます。

## 面白い例: 時間旅行！

想像してみてください。あなたが開発中のプロジェクトで、過去の特定の状態に一時的に「時間旅行」したいと思ったとします。`git switch` と組み合わせて `git restore` を使用することで、過去の特定のコミット状態に瞬時に移動できます。

```bash
# まず過去の安全な場所へ新しいブランチを作成します
git switch -c past-state <コミットハッシュ>
```

これで、過去のコードに触れることができます。修正が終わったら、現在の開発ブランチに戻るだけです。

## よりわかりやすく

`git switch` コマンドは、ブランチ間を移動するためのより直感的な方法を提供します。`git checkout` の複雑さを分割し、使いやすくしています。

## 参考リンク

- [Git switch documentation](https://git-scm.com/docs/git-switch)
- [Git 2.23 のリリースノート](https://github.blog/2019-08-16-highlights-from-git-2-23/)

`git switch` は、Git の使い勝手を向上させる素晴らしいコマンドです。このコマンドを使いこなし、より効率的にブランチを操作しましょう！
