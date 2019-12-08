---
date: 2019-09-27T01:00:48+09:00
title: "Dockerを使う上で最低限覚えておけば良いこと"
keyword: "Docker"
categories: [ "技術系" ]
tags: [ "Docker" ]
draft: false
---

今更ながらDockerを学習中です。
食わず嫌いで今まで触ってこなかったんですが、触ってみると案外簡単でした。
ただ、最初に分かっておけば理解が早かったなーというポイントを見つけたので、ここらで覚え書きを残しておこうと思います。

# ① ざっくりなDockerの仕組み

![Dockerの仕組み](/20190927/how-to-use-docker/img/1.png)

Dockerは、すごく単純に言うと Docker Hub からイメージをダウンロードして、そのイメージからコンテナを生成するだけ。こうやって考えるとかなりシンプルに理解できました。

# ② dockerコマンドとdocker-composeコマンド

Dockerのコマンドには大きく分けると `docker` と `docker-compose` があります。

`docker` が基本のコマンドで、単一のコンテナを使用する分にはこちらで十分使えます。

`docker-compose` は、複数のコンテナを使用する場合にこちらのコマンドを使うことで、より簡単に扱うことができます。
コンテナの設定は `docker-compose.yml` というファイルに記載していきます。

# ③ 超シンプルなDocker起動

[コマンド]

```
docker run centos /bin/echo Hello world
```

[出力結果]

```
Hello ｗorld
```

説明すると、 `docker run centos` までの部分が、CentOSのDockerイメージからコンテナを起動することを表しています。
そして、 `/bin/echo Hello world` の部分は、コンテナの起動後に実行されるコマンドを表しています。
つまり、CentOSのコンテナを起動して、「Hello world」と表示するだけのコマンドです。なので、コンテナも「Hello world」と出力した後は、すぐに停止します。

TODO:
２つのタイトルでそれぞれ記事を書く
「Dockerを使う上で最低限覚えておけば良いこと」
「Dockerをシンプルに始めてみる」
