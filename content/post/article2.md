---
date: 2018-01-17T13:01:33+09:00
title: "Compassを使える環境を整える"
draft: false
categories:  [ "フロントエンド" ]
tags:  [ "CSS", "SCSS(SASS)", "Compass" ]
---

ブログを作成するとなるとCSSをいじることになるのですが、今時CSSを直に書くのは手間なのでCompassを使ってみます。
ちなみにWindows環境です。

## Rubyをインストールする

まずは準備から。
以下のページから RubyInstaller をダウンロードしてきてインストールします。

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

インストールが終わればCompassを使う環境作成は完了です。
と、本来の目的は果たしたわけですが、使い方についても調べてみます。

## Compass利用に必要なファイルを作成

Compassを利用する前にはまず初期化をするみたいですね。
Compassを利用したいディレクトリで以下のコマンドを実行することで、必要なファイルが作成されます。

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
├ sass/
└ config.rb
```

## scssをビルドする

では早速、試しにscssのサンプルコードをビルドしてみます。
まずは、対象のscssファイルを作成して、 `sass` ディレクトリ配下に設置します。

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
├ └ sample.sass
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
├ stylesheet/
│  └ sample.css
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

## おまけ１: エラーでビルド出来ない

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

## おまけ２: ビルド後のcssのコメントが邪魔

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
