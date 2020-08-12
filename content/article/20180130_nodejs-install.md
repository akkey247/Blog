---
date: 2018-01-30T08:37:40+09:00
title: "Node.js(npm)をWindowsにインストールする"
keyword: "Node.js, npm"
categories: [ "技術系" ]
tags: [ "Node.js", "npm" ]
draft: false
---

最近は何をするにしても npm を使ってる気がします。
npm は Node.js のパッケージ管理ツールなんですが、 Node.js 使わないときでもタスクランナー(タスク自動化ツール)として重宝します。
ただ、インストールするたびにやり方を忘れてしまうので、メモを残しておくことにします。
環境はWindowsです。

## nodistをインストール
まずは Node.js をインストールするわけですが、インストール後もバージョンの更新は簡単に行いたいので、バージョン管理ツールは入れておきたいところです。
なので、先に nodist をインストールしておきます。
nodist はインストーラでのインストールになるようなので、インストーラをダウンロードしてきます。

[インストーラ]
https://github.com/marcelklehr/nodist/releases

インストールが終わったら、ちゃんと入っているか確認しておきます。
コマンドプロンプトなどで以下のコマンドを入力して、バージョンが見れたらOK。

```
nodist -v
```

nodist の詳しい使い方については [こちら](https://qiita.com/akkey2475/items/e0ea878a6b955efd9fba) 。

## Node.jsをインストール
本題の Node.js をインストールします。
nodist コマンドを使えば一発でインストール可能です。

今回は最新安定版をイントールしてみます。

```
nodist stable
```

インストールが終わったら、以下のコマンドで確認してみます。

```
node -v
```

バージョンが表示されればOK。

## npm の確認
Node.js が入れば npm は自動でインストールされています。
以下のコマンドで確認してみます。

```
npm -v
```

バージョンが表示されればOKです。

npm の詳しい使い方については [こちら](https://qiita.com/akkey2475/items/4c1eb3e3f36f705c7a1c) 。