# ALMF 公式サイト

ALMF（Academy for Liberal Musical Future）のコンピレーションアルバムプロジェクト公式ウェブサイトです。

🌐 **サイト**: https://almf.info

## ALMF について

"未来の自由な音楽のあり方を探求する音楽コミュニティ"として、ジャンルや既成概念に束縛されない実験的な楽曲創作を通じて、革新的な表現方法を追求しています。

### 主な活動

- **コンピレーションアルバム制作**: M3などの音楽イベント向けに定期リリース
- **イベント参加**: 同人音楽イベントでの頒布と交流
- **オープンコール**: 新規メンバーを定期的に募集
- **実験的プロジェクト**: デジタルファブリケーションと音楽の融合など

## 技術スタック

- **静的サイトジェネレーター**: Jekyll
- **ホスティング**: GitHub Pages
- **テーマ**: pages-themes/minimal
- **Ruby**: 3.4.8（rbenv管理）

## ローカル開発

### 必要な環境

- Ruby 3.4.8 以降（rbenv推奨）
- Bundler

### セットアップ手順

```bash
# Ruby 3.4.8 のインストール（rbenv使用）
rbenv install 3.4.8
rbenv local 3.4.8

# Jekyll のインストール
gem install jekyll

# 依存関係のインストール
cd docs/
bundle install
```

### ローカルサーバー起動

```bash
cd docs/
bundle exec jekyll serve
```

http://127.0.0.1:4000/ でプレビューできます。

### 静的サイトビルド

```bash
cd docs/
bundle exec jekyll build
```

出力先: `docs/_site/`

## トラブルシューティング

### OpenSSL CRL エラー

**症状**: `bundle exec jekyll serve` 実行時に `certificate verify failed (unable to get certificate CRL)` エラー

**原因**: Ruby 3.4.1 ~ 3.4.7 の OpenSSL 実装のバグ

**解決策**: Ruby 3.4.8 以降にアップデート

```bash
anyenv update
rbenv install 3.4.8
rbenv local 3.4.8
bundle install
bundle exec jekyll serve
```

## デプロイ

`main` ブランチへのプッシュにより、GitHub Actions が自動的にビルド・デプロイを実行します。
