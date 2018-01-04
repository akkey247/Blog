---
title: "Hugoでサイト作成"
date: 2017-12-28T16:40:22+09:00
draft: true
---

Hugo でサイト作成をしたので、メモを残します。

OSはWindowsなのであしからず。。。

## Hugo をダウンロードする

以下のページからHugoをダウンロードする。

https://github.com/gohugoio/hugo/releases

ダウンロードしたHugoの「Hugo.exe」を任意のディレクトリに保存する。

```
C:\Hugo\Hugo.exe
```

保存したHugo.exeにはパスをを押しておく。

## サイトを作成する

以下のコマンドを実行する。

```
# hugo new site new_site
```

`new_site` の部分には任意の名前を入力する。

コマンドを実行すると、以下のファイルが作成される。

```
/archetypes
  └ default.md
/content
/data
/layouts
/static
/themes
config.toml
```
test