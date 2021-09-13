# 2. データベースの設定

<!-- toc -->

## 2.1. コンテナを停止

データベースの設定を行うので一度コンテナを停止します。

```yml
docker-compose stop
```

## 2.2. データベースの繋ぎ先を設定

`myapp\config\database.yml`を`database.yml`で上書きします

## 2.3. `default_authentication.cnf`ファイルを配置

`C:\Users\myapp\mysql-confd`に　`default_authentication.cnf`を配置します。

## 2.4. イメージをビルド

```yml
docker-compose build
# 「Successfully built ●●●●●●●●●」が出たら完了！
```

## 2.5. データベース用のコンテナを起動し、データベースの作成

コンテナの起動。

```yml
docker-compose up -d db
```

データベースの作成。

```yml
docker-compose run web rake db:create
```

## 2.6. 全コンテナを起動

上記でデータベースの起動を行ったので，Webアプリケーション側の起動も行います。

```
docker-compose up -d 
```

正常に起動しているかを確認
```
docker ps -a
```
「myapp_web」と「mysql」のコンテナがupしていればOK！
以下に接続してみましょう！

```
http://localhost:3000/
```
![rails](https://user-images.githubusercontent.com/53431136/69325441-85076d80-0c8d-11ea-9610-786f056a8201.png)



