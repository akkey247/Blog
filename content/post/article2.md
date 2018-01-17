---
date: 2018-01-17T13:01:33+09:00
title: "Compassを使える環境を整える"
draft: false
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
@import "compass/utilities/general/clearfix";
.sample {
    @include clearfix;
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
/* line 2, ../sass/test.scss */
.sample {
  overflow: hidden;
  *zoom: 1;
}
```

これでビルド完了です。