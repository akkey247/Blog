---
date: 2018-01-31T08:49:36+09:00
title: "Parcelを使ってみる"
keyword: "Node.js, npm"
categories: [ "技術系" ]
tags: [ "parcel" ]
draft: true
---

最近ビルドツールにParcelを使ってみているので、使い方をまとめてみます。

## 新規プロジェクト作成
まずはnpmでプロジェクトを作成します。

```
npm init -y
```

そして、表示するhtmlファイルを用意します。

```
<html>
<head>
<meta charset="UTF-8">
<title></title>
</head>
<body>
 <!-- Contents -->
</body>
</html>
```

こんな構成になっていると思います。

```
root
├ index.html
└ package.json
```

## パッケージのインストール
Parcelを利用するには `parcel-bundler` パッケージをインストールします。

```
npm install parcel-bundler -D
```

## ビルドする