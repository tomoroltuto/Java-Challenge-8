# 概要
このプロジェクトではDockerによるMySQLの構築をハンズオンしたことをまとめたものです。

# やったこと

* ①Dockerのバージョン確認

* ②cloneしてきたところにdocker-compose.ymlがあることを確認

* ③コンテナを起動と確認

* ④MySQLにログイン

* ⑤データベースにmovie_listがあることを確認

* ⑥movie_listの利用を開始し、テーブルにmoviesテーブルがあることを確認

* ⑦moviesテーブルのレコードを確認

* ⑧テーブルにレコードを追加し登録結果を確認

* ⑨ログアウトする

* ⑩起動したDockerコンテナを停止と停止していることを確認


## ①Dockerのバージョン確認

```bash
% docker -v                             
Docker version 20.10.17, build 100c701
``` 

## ②cloneしてきたところにdocker-compose.ymlがあることを確認
```bash
% ls
Dockerfile		conf			renovate.json
README.md		docker-compose.yml	sql
``` 

## ③コンテナを起動と確認
```bash
 % docker compose up -d
[+] Building 81.5s (8/9)                             
 => [internal] load build definition from Dockerfile            0.0s
 => => transferring dockerfile: 218B                    0.0s
 => [internal] load .dockerignore                     0.0s
 => => transferring context: 2B                      0.0s
 => [internal] load metadata for docker.io/library/mysql:8.0-debian    4.5s
 => [1/4] FROM docker.io/library/mysql:8.0-debian@sha256:6d49fc540dac155 76.9s
...
``` 
```bash
 % docker ps  
CONTAINER ID  IMAGE           COMMAND         CREATED     STATUS     PORTS                NAMES
1781e1cc5f40  docker-mysql-hands-on_db  "docker-entrypoint.s…"  18 seconds ago  Up 12 seconds  33060/tcp, 0.0.0.0:3307->3306/tcp  docker-mysql-hands-on
``` 

## ④MySQLにログイン
```bash
 % docker compose exec db mysql -uroot -p
Enter password: 
Welcome to the MySQL monitor. Commands end with ; or \g.
Your MySQL connection id is 8
Server version: 8.0.30 MySQL Community Server - GPL

Copyright (c) 2000, 2022, Oracle and/or its affiliates.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql>
``` 

## ⑤データベースにmovie_listがあることを確認
```bash
show databases;
+--------------------+
| Database      |
+--------------------+
| information_schema |
| movie_list     |
| mysql       |
| performance_schema |
| sys        |
+--------------------+
5 rows in set (0.01 sec)

mysql>
``` 

## ⑥movie_listの利用を開始し、テーブルにmoviesテーブルがあることを確認

movie_listの利用を開始

```bash
mysql> use movie_list;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
``` 

テーブルにmoviesテーブルがあることを確認

```bash
mysql> show tables;
+----------------------+
| Tables_in_movie_list |
+----------------------+
| movies        |
+----------------------+
1 row in set (0.00 sec)
``` 

## ⑦moviesテーブルのレコードを確認
```bash
mysql> select * from movies;
+----+--------------------------------+-----------------------------+
| id | name              | director          |
+----+--------------------------------+-----------------------------+
| 1 | ショーシャンクの空に      | フランク・ダラボン     |
| 2 | この世界の片隅に        | 片渕須直          |
+----+--------------------------------+-----------------------------+
2 rows in set (0.00 sec)
``` 

## ⑧テーブルにレコードを追加し登録結果を確認

テーブルにレコードを追加

```bash
mysql> insert into movies (name, director) values ("ゴッドファーザー", " フランシス・フォード・コッポラ");
Query OK, 1 row affected (0.02 sec)
``` 
登録結果を確認

```bash
mysql> select * from movies;
+----+--------------------------------+-----------------------------------------------+
| id | name              | director                   |
+----+--------------------------------+-----------------------------------------------+
| 1 | ショーシャンクの空に      | フランク・ダラボン              |
| 2 | この世界の片隅に        | 片渕須直                   |
| 3 | ゴッドファーザー        | フランシス・フォード・コッポラ        |
+----+--------------------------------+-----------------------------------------------+
3 rows in set (0.00 sec)
``` 

## ⑨ログアウトする
```bash
mysql> exit
Bye
``` 

## ⑩起動したDockerコンテナを停止と停止していることを確認

Dockerコンテナを停止

```bash
% docker compose down
[+] Running 2/1
 ⠿ Container docker-mysql-hands-on    Removed             1.3s
 ⠿ Network docker-mysql-hands-on_default Removed             0.1s
``` 
停止していることを確認

```bash
 % docker ps
CONTAINER ID  IMAGE   COMMAND  CREATED  STATUS  PORTS   NAMES
``` 
