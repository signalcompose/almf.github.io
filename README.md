# Jekyllの環境作り

普通にやるなら [公式サイト](https://jekyllrb.com/docs/installation/macos/)のインストールの通りにやればいいのだが `anyenv install rbenv` をして `rbenv install 3.4.1` で入れたrubyを使って行くことにする。また `rbenv local 3.4.1` をルートディレクトリで行いレポジトリ内にのみ有効にする。

ここまで行ったら `ruby -v` でバージョンの確認をする。以下のように変えてくればオッケー。
```
➜   ruby -v
ruby 3.4.1 (2024-12-25 revision 48d4efcb85) +PRISM [arm64-darwin23]
```

次にjekellのインストールを `gem install jekyll` で行う（上記でインストールしたrubyが使えるところでおこまうこと）。`/docs/` 以下で `jekyll new --skip-bundle .` を行うと必要なファイルが作成される（CNAMEの設定を先にしてる場合などは `--force` オプションをつけると良いです）。

基本的には上記は複数で管理する場合には一人がやってれば良いはず（ローカルで見たいとかじゃなければ。markdownのプレビュー自体は別の方法もあるのでその方がお手軽だとは思う。なお上記の手順でjekyllがローカルにインストールされていると `bundle exec jekyll serve` で、ローカルでプレビューできます。）。また `Gemfile` の編集については割愛。

# TBD

