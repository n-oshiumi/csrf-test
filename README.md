# 使用するもの

- php 7.4以上
- mysql
- サーバーはご自由に


# 環境構築

## 専用のデータベースを作成する

ご自身のmysqlで好きな名前のデータベースを作成してください。
この例では、 csrf_phpとします

```sql
CREATE DATABASE csrf_php;
USE csrf_php;
```


## テーブルを作成しデータをいれる

データベースに入って、SQL文でテーブルを作成します。

- ユーザーテーブルを作成

```sql
CREATE TABLE users (id INT(11) AUTO_INCREMENT PRIMARY KEY, email VARCHAR(191),password VARCHAR(191)) engine=innodb default charset=utf8;
```

- ユーザーテーブルにデータをいれる

※パスワードは「password」のハッシュにしている

```sql
INSERT INTO users(email,password) VALUES('test@test.com','$2y$10$UrkWlgzm4TrIFiYEZA9KVeHE3MKlP.uumWK6rxgQ7Q006g0MWTzfi');
INSERT INTO users(email,password) VALUES('hoge@test.com','$2y$10$UrkWlgzm4TrIFiYEZA9KVeHE3MKlP.uumWK6rxgQ7Q006g0MWTzfi');
```

- 投稿(posts)テーブルを作成

```sql
CREATE TABLE posts (id INT(11) AUTO_INCREMENT PRIMARY KEY, user_id INT(11), content TEXT) engine=innodb default charset=utf8;
```

- 投稿テーブルにデータをいれる

```sql
INSERT INTO posts(user_id, content) VALUES(1, 'これは初めての投稿です');
INSERT INTO posts(user_id, content) VALUES(2, 'テスト投稿です');
```

## ライブラリをインストールする
データベースの情報をソースに直書きするわけにはいかないので、 機密情報をenvファイルにいれています。
そのためのライブラリをインストールします。

```bash
composer install
```

## envファイルを作成する
ルートディレクトリ（index.phpと同じ階層）に「.env」という名前のファイルを作成してください
中身はご自身のデータベース情報をいれてください。

```bash
DB_HOST=localhost
DB_NAME=csrf_php
DB_USERNAME=root
DB_PASSWORD=
```

## サーバーを立ち上げてローカル環境で確認する

僕の場合はphpのビルトインサーバーを使用するので下記のコマンドでいけます。
※xamppなど自分が普段使っているものがあればそちらをご使用ください。

```bash
php -S 127.0.0.1:3000
```

これの場合は `http://127.0.0.1:3000` にアクセスして、ログインページが映ればOKです！


【ログイン情報】
メールアドレス: test@test.com
パスワード： password
