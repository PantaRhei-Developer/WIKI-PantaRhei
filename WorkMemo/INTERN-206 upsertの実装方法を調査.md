# 目次

0. [結論](#結論)
1. [概要](#概要)
2. [ワークログ](#ワークログ)
    - [Upsertとは](#upsertとは)
    - [Upsertの実装における選択肢](#upsertの実装における選択肢)

# 0. 結論
Pythonのライブラリpangresのupsert関数でupsertが実装できそう．

# 1. 概要
[INTERN-206: upsertの実装方法を調査完了](https://remotesalesproject.atlassian.net/browse/INTERN-206)

[SQLAlchemy + PostgreSQL で Upsert を行う（ユニークキーに重複があるデータのバルクインサート） - luggage baggage ](https://yoshidabenjiro.hatenablog.com/entry/2017/06/18/152357)

[DataframeをそのままPostgresにUPSERTできちゃうPangres | ShimacoTrip ](https://shimacotrip.com/dataframe%E3%82%92%E3%81%9D%E3%81%AE%E3%81%BE%E3%81%BEpostgres%E3%81%ABupsert%E3%81%A7%E3%81%8D%E3%81%A1%E3%82%83%E3%81%86pangres/)

[pangres ](https://pypi.org/project/pangres/)


# 2. ワークログ
## 2.0. Upsertとは
レコード（行）の挿入を行う際，データがなければそのままINSERTし，既に存在していれば，UPDATEを行うこと．

スクレイピングのデータをDataLakeに挿入する際は，簡潔なためUpsertの実装が好ましい．

## 2.1. Upsertの実装における選択肢
DataUpsertを実装する方法を２つ見つけた．

・[SQLAlchemy + PostgreSQL](https://yoshidabenjiro.hatenablog.com/entry/2017/06/18/152357)

・pangres

pangresはデータベース操作のためのPythonライブラリで，最近開発されたようだ．pangresはpandasの親戚で，DataFrameをpandas.to_sqlのようにレコードの挿入ができるようだ．[DataframeをそのままPostgresにUPSERTできちゃうPangres | ShimacoTrip ](https://shimacotrip.com/dataframe%E3%82%92%E3%81%9D%E3%81%AE%E3%81%BE%E3%81%BEpostgres%E3%81%ABupsert%E3%81%A7%E3%81%8D%E3%81%A1%E3%82%83%E3%81%86pangres/)

元々，テーブルへの挿入にpandas.to_sqlを使用していたため，pangresを試してみる． 

