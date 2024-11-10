---
author: Taro Gray
pubDatetime: 2024-10-08T15:00:00.00Z
title: Gitの変更を取り消す方法まとめ：checkout、reset、restoreを使いこなそう
postSlug: git-discard-changes-guide
featured: true
draft: false
ogImage: https://example.com/git-discard-changes.png
tags:
  - git checkout --
  - git reset
  - git restore
  - git clean -fd

description: Gitでの変更を取り消す方法をわかりやすく解説。checkout、reset、restore の使い方や、特定ファイルの変更の取り消し、ステージングエリアの変更の取り消し、未追跡ファイルの削除など、具体例を交えて説明します。
---

## Table of contents

## 1. git checkout を使った変更の取り消し

git checkout コマンドを使うことで、ファイルの変更を元の状態に戻すことができます。以下のコマンド例を通じて、用途に応じた使い方を学びましょう。

変更を全て破棄する

作業中のすべての変更を取り消して、最後のコミットの状態に戻すには、以下のコマンドを使用します。

git checkout -- .

これを実行すると、modified として表示されていた全てのファイルの変更が破棄され、ワーキングディレクトリがコミット済みの状態に戻ります。

特定のファイルの変更を取り消す

特定のファイルの変更だけを元に戻したい場合には、ファイル名を指定します。

git checkout <ファイル名>

例えば、example.txt の変更を取り消したいときは以下のようにします。

git checkout example.txt

特定のディレクトリ以下の変更を取り消す

特定のディレクトリ配下の変更を再起的に取り消すには、ディレクトリ名を指定します。

git checkout <ディレクトリ名>

例えば、src/ ディレクトリ配下の変更をすべて元に戻したい場合は以下のようにします。

git checkout src/

## 2. git reset を使ったステージングエリアの変更の取り消し

git reset コマンドは、ステージングエリアにあるファイルの変更を取り消すのに使用します。つまり、git add でステージングした変更を元に戻すことができます。

ステージングエリア全体の変更を取り消す

ステージングエリアに追加されたすべてのファイルの変更を取り消すには、以下のコマンドを使用します。

git reset

特定ファイルの変更を取り消す

特定のファイルだけをステージングエリアから取り消したい場合は、ファイル名を指定します。

git reset <ファイル名>

例えば、Gemfile の変更をステージングから取り消す場合は以下のようにします。

git reset Gemfile

## 3. git restore を使った変更の取り消し方法

git restore コマンドは、特定のファイルやディレクトリの変更をワーキングディレクトリまたはステージングエリアから取り消すときに便利です。特に、ファイルごとに取り消し範囲を指定できるのが特徴です。

ファイル全体の変更を取り消す

ワーキングディレクトリ全体の変更を取り消すには、以下のコマンドを使用します。

git restore .

特定のファイルの変更を取り消す

特定のファイルの変更を取り消すには、以下のようにファイル名を指定します。

git restore <ファイル名>

ステージングエリアとワーキングディレクトリの両方の変更を取り消す

以下のコマンドを使用することで、指定したファイルをステージングエリアとワーキングディレクトリの両方から元の状態に戻せます。

git restore --source=HEAD --staged --worktree <ファイル名>

例えば、Gemfile を元の状態に戻したいときは以下のコマンドを実行します。

git restore --source=HEAD --staged --worktree Gemfile

## 4. 未追跡ファイルの取り消しとクリーンアップ

未追跡ファイルとは、Gitがまだ管理していないファイルのことです。以下のコマンドで未追跡ファイルをクリーンアップできます。

未追跡ファイルを削除する

以下のコマンドを使うと、未追跡ファイルを削除できます。

git clean -fd

このコマンドを実行すると、git status に表示されていた Untracked files セクションにあるファイルが削除され、ワーキングディレクトリがクリーンな状態になります。

## 5. まとめ

Gitには、変更を取り消すためのさまざまなコマンドが用意されています。それぞれのコマンドを使いこなすことで、開発作業を効率的に進めることができます。

    •	git checkout: 変更を破棄して、ワーキングディレクトリをコミット状態に戻す。
    •	git reset: ステージングエリアの変更を取り消す。
    •	git restore: ワーキングディレクトリとステージングエリアの特定の変更を取り消す。
    •	git clean: 未追跡ファイルを削除してクリーンアップする。

これらのコマンドを組み合わせて、柔軟にGitの操作を行えるようになりましょう。操作を行う前には、必ず変更内容を確認し、誤った取り消しをしないように注意してください。