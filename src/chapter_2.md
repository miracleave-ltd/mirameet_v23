# 2. データベースの設定

<!-- toc -->

## 2.1. コンテナを停止

データベースの設定を行うので一度コンテナを停止します。

```yml
docker-compose stop
```

## 2.2. データベースの繋ぎ先を設定

`database.yml`ファイルの記述をコピーし、`myapp\config\database.yml`に上書きします。

## 2.3. `default_authentication.cnf`ファイルを配置

`default_authentication.cnf`ファイルを`C:\Users\myapp\mysql-confd`内にコピーします。

## 2.4. イメージをビルド

```yml
docker-compose build
# 「Successfully built ●●●●●●●●●」が出たら完了！
```

## 2.5. データベース用のコンテナを起動し、データベースの作成

コンテナの起動を行います。

```yml
docker-compose up -d db
```

データベースのコンテナに入ります。

```bash
# 起動しているコンテナ名を確認
docker ps
# myapp_db_1というデータベースのコンテナが起動しているのでコンテナへ入る
docker exec -it myapp_db_1 bash
# MySQLにログイン
mysql -u root -p         
Enter password: # passwordを入力
```

MySQLのテーブルを検索し、一部変更する。<br>`Plugin`が`caching_sha2_password`だと後続の手順に影響があるため。
```sql
sql> SELECT User, Host, Plugin  FROM mysql.user;
+------------------+-----------+-----------------------+
| User             | Host      | Plugin                |
+------------------+-----------+-----------------------+
| root             | %         | caching_sha2_password |
| mysql.infoschema | localhost | caching_sha2_password |
| mysql.session    | localhost | caching_sha2_password |
| mysql.sys        | localhost | caching_sha2_password |
| root             | localhost | caching_sha2_password |
+------------------+-----------+-----------------------+
5 rows in set (0.00 sec)
```

以下の通り、SQLを実行して更新。
```sql
mysql> ALTER USER root@localhost IDENTIFIED WITH mysql_native_password BY 'password';
ugin  FROM mysql.user;
Query OK, 0 rows affected (0.01 sec)
```

更新されたか確認する。

```sql
mysql> SELECT User, Host, Plugin  FROM mysql.user;
# 以下のようにrootのPluginがmysql_native_passwordになっていればOK
+------------------+-----------+-----------------------+
| User             | Host      | Plugin                |
+------------------+-----------+-----------------------+
| root             | %         | mysql_native_password |
| mysql.infoschema | localhost | caching_sha2_password |
| mysql.session    | localhost | caching_sha2_password |
| mysql.sys        | localhost | caching_sha2_password |
| root             | localhost | mysql_native_password |
+------------------+-----------+-----------------------+
5 rows in set (0.00 sec)
# exitでMySQLから抜けます
mysql>exit 
```
データベースの作成を行います。

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



