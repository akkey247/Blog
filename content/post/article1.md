---
date: 2017-12-28T16:40:22+09:00
title: "Hugoでブログを作る"
draft: false
categories:  [ "技術系" ]
tags:  [ "Hugo" ]
---

はじめまして、Akkey(アッキー)と申します。
今回、ブログを作成するにあたってHugoという静的サイト生成ツールを利用したので、ブログ作成までの手順をまとめてみました。
ちなみに環境はWindowsです。

## Hugo をダウンロードする

以下のページからHugoをダウンロードします。
自分の環境にあったものをダウンロードしてきてください。

https://github.com/gohugoio/hugo/releases

そして、ダウンロードした圧縮ファイルを展開すると中に `Hugo.exe` という実行ファイルがあるので、任意のディレクトリに保存します。
例えば↓のような感じ。

```
C:\Hugo\Hugo.exe
```

保存したHugo.exeにはパスを通しておきます。

## 新規プロジェクトを作成する

まずは、以下のコマンドを実行。

```
hugo new site new_site
```

`new_site` の部分には任意の名前を入力してください。
コマンドを実行すると、新規プロジェクトが作成されます。
ファイル構成は以下の様な感じになると思います。

```
new_site/
├ archetypes/
├ └ default.md  // 記事の雛形
├ content/    // 記事など
├ data/       // 不明
├ layouts/    // レイアウト(?)
├ static/     // 静的ファイル
├ themes/     // テーマ
└ config.toml // 設定ファイル
```

とりあえず、作成されたプロジェクトのディレクトリに移動しておきます。

```
cd new_site
```

一応この状態でも動くので、確認してみます。
以下のコマンドを実行すると、サーバーが立ち上がりプレビューを確認することができます。

```
hugo server
```

コマンド実行後、 `localhost:1313` にアクセスすると真っ白なサイトが表示されます。
まだ、何も触っていないので真っ白です。

## テーマをダウンロードして適用する

テーマを適用してみます。
以下のサイトから好きなテーマをダウンロードしてきます。

https://themes.gohugo.io/

ダウンロードしたテーマは `themes` ディレクトリの中に入れておいてください。
今回は `hugo_theme_beg` というテーマを使わせていただきました。

https://github.com/dim0627/hugo_theme_beg

```
new_site/
├ archetypes/
├ └ default.md
├ content/
├ data/
├ layouts/
├ static/
├ themes/
├ └ hugo_theme_beg/  // ★ダウンロードしたテーマ
└ config.toml
```

テーマを適用してプレビューするには、以下のコマンドを実行します。

```
hugo server -t hugo_theme_beg
```

まだ、この状態では記事を投稿していないので、記事は表示されません。

## 記事を投稿する

以下のようなコマンドを実行することで記事が投稿できます。

```
hugo new post/newpage.md
```

`newpage.md` の部分は任意の名前を入力してください。
実行すると `content/post` ディレクトリの配下に `newpage.md` が作成されます。
↓のような状態になっていると思います。

```
new_site/
├ archetypes/
├ └ default.md
├ content/
├ └ post/
├   └ newpage.md  // ★作成した記事
├ data/
├ layouts/
├ static/
├ themes/
├ └ hugo_theme_beg/
└ config.toml
```

しかし、このままではプレビューしても記事が表示されないので、プレビューの前に少しページの設定を変更します。
まず、 `newpage.md` を開き `draft: true` を `draft: false` に変更します。これによって下書き状態が解除されます。
(補足すると `---` で括られた部分は記事の設定を書く場所です。)
また、記事の中身が無いので、適当な内容も書いておきます。
とりあえず、おなじみの「Hello World!!」と書いておきました。

```
---
title: "Newpage"
date: 2018-01-01T00:00:00+09:00
draft: false
---

Hello World!!
```

修正を保存して、プレビューしてみると記事が作成されていることが分かります。

## 記事の更新をリアルタイムに反映する

プレビューしている状態で記事の更新がリアルタイムに反映したい時は `-watch` オプションを付けます。
このオプションを付けることによって、記事の更新がリアルタイムに反映されるようになります。

```
hugo server -t hugo_theme_beg -watch
```

と言いたかったのですが、付けなくても反映されるらしいですね。
ちなみに短縮形で `-w` と書いても良いようです。

## サイトをビルドする

実際にサイトをサーバーで稼働させるためにはビルドを行うことになります。
ビルドするには、以下のコマンドを実行します。

```
hugo -t hugo_theme_beg
```

実行すると、 `public` というディレクトリが作成されて、その中にビルドされたサイトが作成されます。

```
new_site/
├ archetypes/
├ └ default.md
├ content/
├ └ post/
├   └ newpage.md
├ data/
├ public/       // ★ビルドされたサイト
├ ├ categories  // カテゴリページ
├ ├ css         // CSSファイル
├ ├ page        // 記事一覧ページ
├ ├ post        // 記事
├ ├ tags        // タグページ
├ ├ 404.html    // 404エラーページ
├ ├ index.html  // トップページ
├ ├ index.xml   // 不明
├ └ sitemap.xml // サイトマップ
├ layouts/
├ static/
├ themes/
├ └ hugo_theme_beg/
└ config.toml
```

この `public` ディレクトリの配下が実際のサイトになります。
`public` ディレクトリの中身をサーバーに置いて、アクセスするとプレビュー時と同じように表示されるはずです。

## 終わりに

実際には、Github Pages を利用してサイト公開までやっているのですが、内容がごちゃごちゃするかなと思い、ここまでの内容に留めました。
Github に上げて公開する手順もまた記事にしたいですね。
コマンドのオプションや設定ファイルの書き方についても、また書いていこうと思います。
それでは！