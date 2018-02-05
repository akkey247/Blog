---
date: 2018-02-05T12:41:39+09:00
title: "heroku ＋ WordPress ＋ PostgreSQL の環境を構築する"
keyword: "heroku, WordPress, PostgreSQL"
categories: [ "技術系" ]
tags: [ "heroku", "WordPress", "PostgreSQL" ]
draft: true
---

HugoでHP作っといてなんですが、WordPress環境作成に挑戦しました。
試しにいじってみるだけの環境なので、無料で出来る構成で作成しようということで、heroku ＋ WordPress ＋ PostgreSQL という構成にしようと思います。
この組み合わせなら [wordpress-heroku](https://github.com/mhoofman/wordpress-heroku) という便利なテンプレートプロジェクトが公開されているのですが、対応が4.1.1までだったので断念しました。
ということで、最新の WordPress 4.9.2 で構築を目指してみます。

## GitHubでリポジトリ作成する
リモートリポジトリはGitHubを使います。
GitHubでリポジトリを作成して、ローカル環境へクローンしておきます。

## heroku にアプリを作成する


## heroku に PostgreSQL アドオンをインストールする

## WordPress最新版をダウンロードする
いよいよWordPressをダウンロードします。
↓ここから最新版(4.9.2)をダウンロードしてきます。

https://ja.wordpress.org/

ダウンロードしたWordPressはGitリポジトリにコミットしておきます。

## wp-config.phpを編集する
次に wp-config.php を編集します。
`wp-config-sample.php` を `wp-config.php` にリネームして使ってください。
wp-config.phpの内容は例の [wordpress-heroku](https://github.com/mhoofman/wordpress-heroku) を参考にさせていただきました。

以下の2箇所を修正します。
これでサーバーから情報を拾ってきてくれるようです。

```
$db = parse_url($_ENV["DATABASE_URL"]);

/** WordPress のためのデータベース名 */
define('DB_NAME', trim($db["path"],"/"));

/** PostgreSQL データベースのユーザー名 */
define('DB_USER', $db["user"]);

/** PostgreSQL データベースのパスワード */
define('DB_PASSWORD', $db["pass"]);

/** PostgreSQL のホスト名 */
define('DB_HOST', $db["host"]);

/** データベースのテーブルを作成する際のデータベースの文字セット */
define('DB_CHARSET', 'utf8');

/** データベースの照合順序 (ほとんどの場合変更する必要はありません) */
define('DB_COLLATE', '');
```

```
define('AUTH_KEY',              getenv('AUTH_KEY'));
define('SECURE_AUTH_KEY',       getenv('SECURE_AUTH_KEY'));
define('LOGGED_IN_KEY',         getenv('LOGGED_IN_KEY'));
define('NONCE_KEY',             getenv('NONCE_KEY'));
define('AUTH_SALT',             getenv('AUTH_SALT'));
define('SECURE_AUTH_SALT',      getenv('SECURE_AUTH_SALT'));
define('LOGGED_IN_SALT',        getenv('LOGGED_IN_SALT'));
define('NONCE_SALT',            getenv('NONCE_SALT'));
define('AWS_ACCESS_KEY_ID',     getenv('AWS_ACCESS_KEY_ID'));
define('AWS_SECRET_ACCESS_KEY', getenv('AWS_SECRET_ACCESS_KEY'));
```

## pg4wpプラグインをインストールする
次にPostgreSQLを利用するために、pg4wpプラグインをインストールします。
とりあえずここからプラグインをダウンロードしてきます。

https://github.com/kevinoid/postgresql-for-wordpress

ちなみにこのpg4wpプラグインは本家から別の方が一時的にフォークして更新したものみたいです。
本家の方は WordPress 3.4.2 までしかサポートしていないためこっちを使っています。
本家 ⇒ https://ja.wordpress.org/plugins/postgresql-for-wordpress/

ダウンロードしてきたら、まずは中の `pg4wp` というディレクトリを `wp-content/` 配下に配置します。
そして `pg4wp` 内の `db.php` というファイルを `wp-content/` 配下に移動します。
↓こんな感じの配置になります。

```
wp-content/
├ languages/
├ pg4wp/      // ★pg4wp本体
├ plugins/
├ themes/
├ db.php      // ★pg4wp呼び出し用ファイル
└ index.php
```

## heroku にデプロイする
上で編集したソースを GitHub へ push したら、heroku 上でデプロイします。

## アプリを起動して、WordPressをインストールする

