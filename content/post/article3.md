---
title: "Hugoで作ったブログをGitHub Pagesで公開する"
date: 2018-01-18T12:19:52+09:00
draft: false
categories:  [ "フロントエンド" ]
tags:  [ "GitHub Pages", "Hugo" ]
---

以前書いた [Hugo でブログを作る](/post/article1/) という記事で作ったブログサイトを GitHub Pages で公開するまでの方法を書いてみます。

## GitHubで新規リポジトリを作成する

まずは、GitHubでリポジトリを作成します。
仮に `Blog` という名前のリポジトリで作成してみます。

作り終わったら、ローカル環境へクローンしてきます。

```
git clone git@github.com:ユーザー名/Blog.git
```

クローンした空のソースの中に Hugo で作成したサイトをコピーしてきます。
後述しますが、一旦 `public` ディレクトリは一旦消しています。

こんな構成になります。
(サブディレクトリの中身は若干端折ってます。)

```
Blog/
├ archetypes/
├ content/
├ data/
├ layouts/
├ static/
├ themes/
├ └ hugo_theme_beg/  // 前の記事で使ったテーマ
└ config.toml
```

一旦、コミットしておきます。

## 公開用ディレクトリを作成する

Hugoでビルドした際に自動で生成されるディレクトリは `public` でしたが、
GitHub Pagesでは公開ディレクトリは `docs` という名前にしなくてはいけません。
なので、ビルドする際にディレクトリ名を指定することにします。

ディレクトリ名を指定してビルドするには、コマンドに `-d ディレクトリ名` と追加します。
早速ディレクトリ名に `docs` を指定してビルドしてみます。

```
hugo -t hugo_theme_beg -d docs
```

`docs` という名前でディレクトリが作成されたと思います。

```
Blog/
├ archetypes/
├ content/
├ data/
├ docs/     // ★作成された
├ layouts/
├ static/
├ themes/
└ config.toml
```

## GitHub Pagesへ反映する

まずは、作ったソースをリモートリポジトリへプッシュします。

プッシュが終わったら、GitHubから設定を変更します。

GitHubのリポジトリページから setting > GitHub Pages を開きます。
None と書いてあるプルダウンメニューがあるので、そこを開いて「master branch/docs folder」を選びます。
選択したら「Save」ボタンを押してください。
これで準備OKです。

## ブログを確認する

`https://ユーザー名.github.io/Blog/` のURLにアクセスすればページが表示されるはずです。

## 終わりに

本当はHugoで作ったプロジェクトをローカルリポジトリとして初期化してからリモートに上げる流れがスムーズなのかもしれないですね。
こっちの方が楽そうだったので、このやり方で反映してみました。