---
author: LIL JAP KID
pubDatetime: 2023-10-28T00:37:54.547Z
title: これはテストです。
postSlug: astro-paper-v4
featured: true
ogImage: https://github.com/satnaing/astro-paper/assets/53733092/1ef0cf03-8137-4d67-ac81-84a032119e3a
tags:
  - release
description: "これはテストです。はつ投稿です。"
---

## Tabel of contents

## 特徴 & 変更点 (Features & Changes)

### Astro v3との統合 (Astro v3 Integration)

<video autoplay loop="loop" muted="muted" plays-inline="true">
  <source src="https://github.com/satnaing/astro-paper/assets/53733092/18fdb604-1ca3-41a0-8372-1367759091ff" type="video/mp4">
  <!-- <source src="/assets/docs/astro-paper-v3-view-transitions-demo.mp4" type="video/mp4"> -->
</video>

AstroPaperは現在、[Astro v3](https://astro.build/blog/astro-3/)を完全にサポートし、性能とレンダリング速度が向上しています。

また、ビュー間の魅力的でダイナミックなトランジションを作成できるように、Astroの[ViewTransitions API](https://docs.astro.build/en/guides/view-transitions/)に対するサポートを追加しました。

「最近のセクション」では、重複を避け、ViewTransitions APIをより適切にサポートするために、注目されていない投稿のみが表示されます。

### OGイメージ生成ロジックの更新 (Update OG Image Generation Logic)

![Example OG Image](https://user-images.githubusercontent.com/40914272/269252964-a0dc6735-80f7-41ed-8e74-4d4d70f96891.png)

自動OGイメージ生成のロジックを更新し、より信頼性が高く効率的になりました。さらに、投稿タイトルに特殊文字が含まれている場合でも、正確で柔軟で目を引くソーシャルメディアのプレビューを提供します。

`SITE.ogImage`は現在オプションです。指定されていない場合、AstroPaperは`SITE.title`、`SITE.desc`および`SITE.website`を使用してOGイメージを自動生成します。

### テーマメタタグの追加 (Theme meta tag)

theme-colorメタタグを追加し、テーマの切り替えに動的に適応することで、シームレスなユーザーエクスペリエンスを実現しています。

> 上部の違いに注目してください

**_AstroPaper v2 テーマ切り替え_**

<video autoplay loop="loop" muted="muted" plays-inline="true">
  <source src="https://github.com/satnaing/astro-paper/assets/53733092/3ab5a1e8-1891-4264-a5bb-0ded69143c1a" type="video/mp4">
</video>

**_AstroPaper v3 テーマ切り替え_**

<video autoplay loop="loop" muted="muted" plays-inline="true">
  <source src="https://github.com/satnaing/astro-paper/assets/53733092/8ac9deb8-d1f8-4029-86bd-6aa0def380b4" type="video/mp4">
</video>

## その他の変更点 (Other Changes)

### Astro Prettier プラグイン (Astro Prettier Plugin)

Astro Prettier プラグインは、プロジェクトを整理整頓し続けるために初めからインストールされています。

### マイナースタイルの変更 (Minor Style Changes)

単一行のコードブロックのラッピング問題が解決され、コードスニペットがきれいに表示されるようになりました。

ナビゲーションスタイルのCSSを更新して、ナビゲーションにさらにリンクを追加できるようにしました。

## AstroPaper v3へのアップグレード (Upgrade to AstroPaper v3)

> このセクションは、古いバージョンからAstroPaper v3にアップグレードを希望する方向けです。

このセクションは、AstroPaper v2からAstroPaper v3への移行を支援します。

このセクションの残りの部分を読む前に、依存関係とAstroPaperをアップグレードする方法に関する[この記事](https://astro-paper.pages.dev/posts/how-to-update-dependencies/)をチェックすることをお勧めします。

## オプション1: 新規スタート（推奨） (Option 1: Fresh Restart (recommended))

このリリースでは多くの変更があり、古いAstro APIの置き換え、バグ修正、新機能の追加などが行われています。したがって、あまりカスタマイズをしていない方は、この方法を採用すべきです。

**_ステップ1: すべての更新済みファイルを保持_**

既に更新されているファイルをすべて保持することが重要です。これらのファイルには以下が含まれます。

- `/src/config.ts` (v3では変更なし)
- `/src/styles/base.css` (v3でわずかな変更; 下記参照)
- `/src/assets/` (v3では変更なし)
- `/public/assets/` (v3では変更なし)
- `/content/blog/` (これはあなたのブログコンテンツのディレクトリです 🤷🏻‍♂️)
- その他のカスタマイズされたファイル

**_ステップ2: 旧プロジェクトのクローン_**

新しいディレクトリで、AstroPaper v3テンプレートの最新版をクローンします。

```bash
npm init astro --template astro-paper
```
