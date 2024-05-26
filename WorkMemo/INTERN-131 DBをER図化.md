# 目次

0. [結論](#結論)
1. [概要](#概要)
2. [ワークログ](#ワークログ)

# 0. 結論
 
# 1. 概要
[INTERN-131: DBをER図化完了](https://remotesalesproject.atlassian.net/browse/INTERN-131)
 

# 2. ワークログ
[【Docker Desktop】Macにインストール【Monterey/M1】 ](https://chigusa-web.com/blog/docker-desktop-mac/)

これを参考にdocker環境を作った。

[【Docker】PostgreSQLの起動時に初期データをセットアップ ](https://amateur-engineer.com/docker-compose-postgresql/)

これを参考にpostgreSQLを使えるようにした。

https://tyotto-good.com/db/schemaspy

これを参考にER図化を進める。

```
WARNING: The requested image's platform (linux/amd64) does not match the detected host platform (linux/arm64/v8) and no specific platform was requested
Running Main-Class org.springframework.boot.loader.JarLauncher
With drivers:jtds-1.3.1.jar, mariadb-java-client-1.1.10.jar
mysql-connector-java-6.0.6.jar, postgresql-42.1.1.jre7.jar
```

以上のようなコードが出た。

解決策

[docker compose 上で SchemaSpy が動かないのを直す (MySQL 8, Apple M1 Mac) - Qiita ](https://qiita.com/mikankari/items/785cb00d8b7b1f563f13)

上記のサイトをもとに試してみる。

エラーが出て解決しなかったので違う方法を試してみる。


[DockerでPostgreSQLとSchemaSpyを使ってDBドキュメントを作成する（Apple M1チップ編） - Qiita ](https://qiita.com/fakefurcoronet/items/f44ee24c94bcfc4ca6bb)

上記を参考にやってみた。

しかしpgadminのところで何故か引っかかる。


[【Docker】PostgreSQLの起動時に初期データをセットアップ ](https://amateur-engineer.com/docker-compose-postgresql/)

自分の環境でデータベースを作らないといけないので上記のサイトを参考にし作る。
