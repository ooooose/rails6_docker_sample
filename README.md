# Dockerを用いたrails6の環境構築
## 技術構成
以下の環境をローカルに構築
- rails6
- mysql@8

## 構築手順
クローン後に以下のコマンドを実行。
```
docker-compose run --no-deps app rails new . --force --database=mysql --skip-test --skip-spring
```

ビルド後は`config/database.yml`の以下を修正する。<br />
```
## 中略

default: &default
  adapter: mysql2
  encoding: utf8mb4
  pool: <%= ENV.fetch("RAILS_MAX_THREADS") { 5 } %>
  username: root
  password: password # ここと
  host: db #ここを修正（docker-composeで作成したコンテナ名に変更(db)）

## 以下略
```

以下のコマンドを実行してデータベースを作成する。
```
docker-compose exec app rails db:create
```
問題なく作成できたら、以下のコマンドで立ち上げる。
```
docker-compose up -d
```
`-d`オプションをつけるとバックグラウンドで実行される。ただなくても良い。

## 成功画面(localhost3000)

