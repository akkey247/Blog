---
date: 2018-01-17T13:01:33+09:00
title: "Compass を利用できる環境を作る"
draft: false
---

## Ruby をインストール

以下のページから RubyInstaller をダウンロードし、インストールする
https://rubyinstaller.org/

備考
・Td/Tk サポートのインストールはチェックしなくてもよい
・Rubyの実行ファイルへパスを通す設定にチェックしておく
・.rb,.rbwのファイル関連付け設定のチェックは任意

## Compass をインストール

### コマンドプロンプトで以下のコマンドを実行

```
gem update --system
gem install compass
```

## compass の初期化

### コマンドプロンプトで以下のコマンドを実行
コマンドプロンプトで Compass を利用したいディレクトリまで移動して以下のコメンドを実行

```
compass create
```

最小限の構成で初期化したい場合は以下のコマンドを使う

```
compass create --bare
```

コマンド実行後、以下のディレクトリが作成されていれば成功
```
root
├ sass/
└ config.rb
```

## compass でビルドしてみる

試しにサンプルコードをビルドしてみる。

### sassディレクトリ配下にサンプルコードのファイルを配置する。

test.scss
```
@import "compass/utilities/general/clearfix";
.sample {
    @include clearfix;
}
```

### 以下のコマンドを実行

```
compass watch
```

コマンド実行後、stylesheet/, .sass-cache/ のディレクトリが作成され、 stylesheet/ 配下にサンプルコードのビルド結果ファイルが格納される
```
root
├ .sass-cache/
├ sass/
│  └ test.scss
├ stylesheet/
│  └ test.css
└ config.rb
```

test.scss
```
/* line 2, ../sass/test.scss */
.sample {
  overflow: hidden;
  *zoom: 1;
}
```
test