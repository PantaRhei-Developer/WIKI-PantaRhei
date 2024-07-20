# 目次

1. [ゴール](#ゴール)
2. [概要](#概要)
3. [ワークログ](#ワークログ)

# 0. ゴール
Insertの実装を組み入れて，週次バッチ化成功させる．

# 1. 概要
[INTERN-238: UpsertからInsertの実装に変更完了](https://remotesalesproject.atlassian.net/browse/INTERN-238)
 

UpsertでDBのテーブルへデータ挿入に成功したが，データが多くなるほど，レコードの挿入に時間がかかる．レコードの挿入時に，既存のレコードの中に，挿入予定のレコードと同じ複合主キーのレコードがあるか検索するのに時間がかかるからだ．また，Upsertでの実装では複合主キーのどれか1つでもないと挿入されないため，欠損データの分析ができなくなる．

また，Upsert実装時の課題であったコストの壁は，弊社がGoogle for Startupsの認定を受けているため，クリアされている．

そのため，Insertでの実装に仕様変更した．


このエピックでは以下のことを行う．

GCEが週次で起動し，スクレイピングを実行する.

その後はCloudStorageにjsonファイルを移動させ，DBにinsertする．

# 2. ワークログ
[INTERN-243 insertに合わせてテーブル作成するsql文の変更](https://github.com/PantaRhei-Developer/WIKI-PantaRhei/blob/main/WorkMemo/INTERN-243%20insert%E3%81%AB%E5%90%88%E3%82%8F%E3%81%9B%E3%81%A6%E3%83%86%E3%83%BC%E3%83%96%E3%83%AB%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8Bsql%E6%96%87%E3%81%AE%E5%A4%89%E6%9B%B4.md)

[INTERN-256 リージョンとUTCオフセットの紐付けjsonをqiitaに上げる](https://github.com/PantaRhei-Developer/WIKI-PantaRhei/blob/main/WorkMemo/INTERN-256%20%E3%83%AA%E3%83%BC%E3%82%B8%E3%83%A7%E3%83%B3%E3%81%A8UTC%E3%82%AA%E3%83%95%E3%82%BB%E3%83%83%E3%83%88%E3%81%AE%E7%B4%90%E4%BB%98%E3%81%91json%E3%82%92qiita%E3%81%AB%E4%B8%8A%E3%81%92%E3%82%8B.md)
  
