# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ALMF公式サイト - Jekyll製の静的サイト（GitHub Pages）で、ALMFの活動記録と音楽作品のカタログを公開しています。

- **サイトURL**: https://almf.info
- **技術スタック**: Jekyll + GitHub Pages
- **Ruby バージョン**: 3.4.8（rbenv管理、OpenSSL CRL 修正版）
- **テーマ**: pages-themes/minimal (remote theme)

## Development Setup

### 初回セットアップ

```bash
# Ruby 3.4.8のインストール（rbenv使用）
rbenv install 3.4.8
rbenv local 3.4.8

# Jekyllのインストール
gem install jekyll

# 依存関係のインストール
cd docs/
bundle install
```

### 主要コマンド

```bash
# ローカル開発サーバーを起動（http://localhost:4000）
cd docs/
bundle exec jekyll serve

# 静的サイトをビルド（出力先: docs/_site/）
cd docs/
bundle exec jekyll build

# 依存関係の更新
cd docs/
bundle update
```

## Project Structure

```
almf.github.io/
├── docs/                    # Jekyllプロジェクトルート
│   ├── _config.yml         # Jekyll設定
│   ├── _data/              # データファイル
│   │   └── albums.yml      # アルバムカタログデータ（データ駆動）
│   ├── _includes/          # 再利用可能コンポーネント
│   │   ├── album_grid.html # アルバムグリッド表示（albums.ymlから自動生成）
│   │   └── head-custom.html
│   ├── _layouts/           # カスタムレイアウト
│   │   └── default.html    # メインレイアウト（ナビゲーション含む）
│   ├── _posts/             # ブログ記事（YYYY-MM-DD-title.markdown形式）
│   ├── _site/              # ビルド出力（.gitignore対象）
│   ├── about.markdown      # Aboutページ
│   ├── archive.markdown    # アーカイブページ
│   ├── catalog.markdown    # カタログページ
│   ├── events.markdown     # イベントページ
│   ├── opencall.markdown   # Open Callページ
│   └── index.markdown      # トップページ
├── assets/                  # 静的アセット（画像、CSS、JSなど）
│   └── images/             # 画像ファイル（ブログ記事用画像など）
├── .github/
│   └── workflows/
│       └── jekyll-gh-pages.yml  # GitHub Actions自動デプロイ設定
└── README.md               # 開発環境構築手順
```

## Architecture

### データ駆動型カタログシステム

アルバム情報は`_data/albums.yml`で一元管理され、`_includes/album_grid.html`コンポーネントで自動的にグリッド表示されます。

**新しいアルバムの追加手順**:
1. `docs/_data/albums.yml`に新規エントリを追加
   ```yaml
   - title: "アルバム名"
     date: "YYYY-MM-DD"
     image: "https://example.com/image.jpg"
     url: "https://bandcamp.com/album/..."
   ```
2. カタログページ（`docs/catalog.markdown`）は自動的に更新される

### カスタムレイアウト

`_layouts/default.html`は以下の機能を提供:
- サイドバーナビゲーション（About, Events, Catalog, Archive）
- ソーシャルリンク（Twitter, Bandcamp, RSS）
- 現在のページのハイライト（`{% if page.url == ... %}`）

### ブログ記事

- ファイル名: `YYYY-MM-DD-タイトル.markdown`
- フロントマター必須: `layout`, `title`, `date`, `categories`
- Archiveページで自動的に一覧表示

## Deployment

### GitHub Actions自動デプロイ

- **トリガー**: `main`ブランチへのプッシュ
- **ワークフロー**: `.github/workflows/jekyll-gh-pages.yml`
- **ビルド**: GitHub Actionsが`docs/`ディレクトリをビルド
- **デプロイ**: GitHub Pagesに自動デプロイ

**注意**: `main`ブランチへのプッシュ後、デプロイ完了まで数分かかります。

## Git Workflow

- **メインブランチ**: `main`
- **コミットメッセージ**: 英語タイトル、日本語本文
- **現在の運用**: ブランチプロテクションは未設定のため、`main` ブランチへの直接プッシュが可能
  - 将来的に、feature ブランチ → PR → レビュー → main マージのワークフローへ移行を推奨

### コードレビューワークフロー

**コミット前のコードレビュー**（Claude Code の hook で強制）:

```bash
# 1. 変更をステージング
git add <files>

# 2. コードレビュー実行
/code:review-commit

# 3. レビュー完了後、コミット
git commit -m "commit message"
```

**レビュープロセス**:
- pr-review-toolkit:code-reviewer エージェントが自動レビュー
- critical/important 問題を検出・報告
- レビュー承認後、approve-review.sh スクリプトが承認ハッシュを保存
- Claude Code の hook が承認ハッシュを検証してコミット許可

**注意**:
- コミット前に必ず `/code:review-commit` を実行すること
- Claude Code 使用時、コードレビューが自動的に要求される
- レビュー未実施の場合、コミット時にエラーが表示される

## Common Tasks

### 新しいブログ記事を作成

```bash
# docs/_posts/ に新規ファイルを作成
# ファイル名: YYYY-MM-DD-title.markdown

---
layout: post
title: "記事タイトル"
date: YYYY-MM-DD HH:MM:SS +0900
author: ALMF
categories: news events
tags: [タグ1, タグ2, タグ3]
---

記事本文をここに書く...
```

**フロントマターフィールド**:
- `layout`: 必須（通常は `post`）
- `title`: 記事タイトル
- `date`: 公開日時（タイムゾーン `+0900` 必須）
- `author`: 著者名（記事に "by 著者名" と表示される）
- `categories`: カテゴリ（スペース区切り、例: `news events`）
- `tags`: タグリスト（`[tag1, tag2, tag3]` 形式）

**画像の追加**:
1. 画像を `assets/images/` ディレクトリに配置
2. 記事内で `/assets/images/filename.jpg` として参照
3. 画像の回り込みを防ぐには HTML + CSS を使用:
   ```html
   <div style="margin: 20px 0;">
     <img src="/assets/images/image.jpg" alt="説明"
          style="width: 100%; max-width: 600px; display: block; margin: 0 auto;">
   </div>
   ```

**注意事項**:
- 画像パスは `/assets/images/` で始める（`docs/` は含めない）
  - Jekyll ビルド後のパスを使用（`baseurl` が空のため `/` から始まる）
  - 実際のファイル配置: `assets/images/filename.jpg`
  - 記事内参照: `/assets/images/filename.jpg`
- タグは YAML リスト形式 `[tag1, tag2]` で記述
- `author` フィールドがないと著者名が表示されない

### 新しいアルバムをカタログに追加

```bash
# docs/_data/albums.yml を編集
# リストの先頭に追加（最新アルバムが上に表示される）

- title: "New Album Title"
  date: "YYYY-MM-DD"
  image: "https://..."
  url: "https://..."
```

### サイト設定の変更

```bash
# docs/_config.yml を編集
# title, description, url, email などを変更可能
# 変更後は Jekyll サーバーの再起動が必要
```

## Important Notes

- **作業ディレクトリ**: コマンドは`docs/`ディレクトリで実行（Jekyllプロジェクトルート）
- **_config.yml変更時**: `bundle exec jekyll serve`を再起動しないと反映されない
- **Ruby バージョン**: `.ruby-version`で3.4.8を指定済み（rbenv使用）
- **依存関係**: `github-pages` gem により GitHub Pages 互換性を保証

## Troubleshooting

### OpenSSL CRL エラー（`certificate verify failed unable to get certificate CRL`）

**症状**: `bundle exec jekyll serve` 実行時に SSL 証明書エラーが発生

**原因**: Ruby 3.4.1 ~ 3.4.7 の OpenSSL 実装に CRL（証明書失効リスト）チェックのバグがある

**解決策**: Ruby を 3.4.8 以降にアップデート

```bash
# ruby-build を最新化
anyenv update

# Ruby 3.4.8 をインストール
rbenv install 3.4.8
rbenv local 3.4.8

# 依存関係を再インストール
bundle install

# Jekyll を起動
bundle exec jekyll serve
```

**参考**: この問題は Ruby のパッチバージョンで修正されており、OpenSSL 3.x 自体の問題ではありません
