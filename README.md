# CakePHP4 Docker環境構築

## ディレクトリ構成
```tree
├── docker
│   ├── mysql
│   │   ├── my.cnf  # MySQLの設定ファイル
│   │   └── db      # データベース永続化用ディレクトリ
│   └── php
│       └── Dockerfile
├── .env
├── .gitignore
└── docker-compose.yml
```

## 手順
1.コンテナの構築
$ docker-compose up -d --build

2.PHPコンテナ情報の確認
$ docker ps

3.PHPコンテナに入りcakephp4のインストール
(例)$ docker exec -it cakephp4-php-1 bash

4.cakephpのインストール(結構時間がかかります)
$ cd ../
$ composer create-project --prefer-dist cakephp/app:4.* html

5.cakephpの初期設定
```app_local.php
config > app_local.phpの編集
Datasources' => [
        'default' => [
            'host' => 'db', # dbコンテナ名
            /*
             * CakePHP will use the default DB port based on the driver selected
             * MySQL on MAMP uses port 8889, MAMP users will want to uncomment
             * the following line and set the port accordingly
             */
            //'port' => 'non_standard_port_number',

            'username' => '.envに書いてあるユーザー名',
            'password' => '.envに書いてあるパスワード',

            'database' => '.envに書いてあるDB DB名',
```
6.動作確認
cakephp4 http://localhost:9811
phpmyadmin http://localhost:9831