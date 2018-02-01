---
date: 2018-01-17T13:01:33+09:00
title: "Compassを使える環境を整える"
keyword: "Compass, CSS, SCSS(SASS)"
description: "Compassを使える環境を整える"
categories: [ "技術系" ]
tags: [ "CSS", "SCSS SASS", "Compass" ]
draft: false
---

ブログを作成するにあたってCSSを触っているのですが、CSSのまま編集するとかなり手間なので、この機会にSass(SCSS)とCompassを利用してみることにしました。
今回も環境はWindowsです。

## Rubyをインストールする

まずは準備から。
以下のページから RubyInstaller をダウンロードし、インストールします。

https://rubyinstaller.org/

[インストール時のメモ]
・Td/Tk サポートのインストールはチェックしなくてもOK
・Rubyの実行ファイルへパスを通す設定にチェックしておく
・.rb,.rbwのファイル関連付け設定のチェックは任意

## Compassをインストールする

Rubyのインストールが終わったら、早速Compassをインストールします。
コマンドプロンプトで以下のコマンドを実行します。

```
gem update --system
gem install compass
```

インストールが終わったら、ちゃんと入っているか確認してみます。

```
compass -v
```

これでバージョンが表示されればOK、Compassを使う環境作成は完了です。
と、本来の目的は果たしたわけですが、ここから使い方についても調べてみます。

## Compassの新規プロジェクト作成

Compassを利用する前にはまず新規プロジェクトを作る必要があるようですね。
Compassを利用したいディレクトリで以下のコマンドを実行することで、新規プロジェクトが作成されます。

```
compass create
```

最小限の構成で初期化したい場合は `--bare` オプションを付けると良いようです。

```
compass create --bare
```

実行後、以下のディレクトリが作成されていれば成功です。(ちなみに `--bare` オプション有りの場合です。)

```
root
├ sass/      // Sass(SCSS)ファイルが入るディレクトリ
└ config.rb  // Compass設定ファイル
```

## scssをビルドする

では早速、試しにSCSSのサンプルコードをビルドしてみます。
まずは、対象のSCSSファイルを作成して、 `sass` ディレクトリ配下に設置します。

sample.scss
```
@import 'compass';
.sample {
  @include border-radius(3px);
}
```

```
root
├ sass/
├ └ sample.sass  // ★追加したファイル
└ config.rb
```

ビルドをしてみます。
以下のコマンドを実行。

```
compass watch
```

実行すると、 `stylesheet/` , `.sass-cache/` ディレクトリが作成されます。
`stylesheet/` ディレクトリ配下にサンプルコードのビルド結果ファイルが格納されます。

```
root
├ .sass-cache/
├ sass/
│  └ sample.scss
├ stylesheet/    // ★ビルド後のCSSが入るディレクトリ
│  └ sample.css  // ★CSSファイル
└ config.rb
```

sample.css
```
/* line 2, ../sass/sample.scss */
.sample {
  -moz-border-radius: 3px;
  -webkit-border-radius: 3px;
  border-radius: 3px;
}
```

これでビルド完了です。

## エラーでビルド出来ない時

最初ビルドがうまく動かない時がありました。
エラーメッセージにはこんな表示が。

```
Error: Invalid Windows-31J character
```

調べてみると `config.rb` に以下の１行を追加することでビルド出来るようになるようです。

```
Encoding.default_external = 'utf-8'
```

[参考]
[Windows環境のcompassで”Invalid Windows-31J character”のエラー](http://blog.a4works.co.jp/archives/326)

## ビルド後のcssのコメントが邪魔な時

個人的にビルドされたCSSに入る↓このコメントが邪魔だったので、消す方法を探してみました。
どうやら、元々 `config.rb` に書いてある `# line_comments = false` をコメント解除すれば良いみたいですね。

```
require 'compass/import-once/activate'

http_path = "/"
css_dir = "stylesheets"
sass_dir = "sass"
images_dir = "images"
javascripts_dir = "javascripts"

# ビルド後のコメント非表示
line_comments = false
```
