# 目次

- [0. 結論](#0-結論)
- [1. 概要](#1-概要)
- [2.ワークログ](#2-ワークログ)
   - [保存の仕方](#保存の仕方)
   - [方法の理由](#方法の理由)



# 0. 結論
スクリーンによって、僕のパソコンが動いていなくても、インスタンス上でスクレイピングすることができた。

# 1. 概要
[pandas.DataFrame.to_sql — pandas 2.2.2 documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_sql.html)

[INTERN-123: GCS内のjsonをCloudSQLにインポートできるサービスを調査完了](https://remotesalesproject.atlassian.net/browse/INTERN-123)
 

# 2. ワークログ

## 保存の仕方
json、DataFrame、SQLで保存
様々なサイトを調査した結果，Pythonのpandas.to_sqlを使用する方法がシンプルに思えたため，DataFrameを経由してSQLに保存することにした．

## 方法の理由
jsonからPostgreSQLへの保存方法はいくつかあり，他の方法はインスタンス上にjsonファイルがある必要がある．

DataFrameを挟む方法を取る理由はここにある．GCEでスクレイピングの結果（jsonファイル）をStorageに入れたあとに，またStorageからインスタンス上にダウンロードをするのはきれいな形ではない．

一方，Pandasのread_jsonはインスタンス上にjsonファイルが無くても，StorageからDataFrameにすることが可能だ．

結論を言うと，「GCE→GCS→SQL」の流れをきれいに実現できる方法だから，DataFrame経由の方法を選択した．

