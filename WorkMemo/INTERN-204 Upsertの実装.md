# 目次

1. [ゴール](#ゴール)
2. [概要](#概要)
3. [ワークログ](#ワークログ)

# 0. ゴール
Upsertの実装を組み入れて，週次バッチ化成功させること．

# 1. 概要
[INTERN-170: jsonファイルをCloud SQLに追加完了](https://remotesalesproject.atlassian.net/browse/INTERN-170)
 
「INTERN-170 jsonファイルをCloud SQLに追加」では，pandas.to_sqlを使用してDataFrameをデータベースのテーブルへ挿入する実装をしていた．

to_sqlの引数”if_exits“では，テーブルが既に存在する場合の挙動を「”fail", "replace", "append“」から選択できる．[pandas.DataFrame.to_sql — pandas 2.2.2 documentation](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.to_sql.html)

しかし，レコード単位で存在しているかチェックすることはできないため，pandas.to_sqlではUpsertの実装が不可能だ．
そこで，本エピックでは，別の方法でテーブルにデータをUpsertすることを扱う．

[INTERN-204: Upsertの実装完了](https://remotesalesproject.atlassian.net/browse/INTERN-204)

# 2. ワークログ
[INTERN-206 upsertの実装方法を調査](https://github.com/PantaRhei-Developer/WIKI-PantaRhei/blob/main/WorkMemo/INTERN-206%20upsert%E3%81%AE%E5%AE%9F%E8%A3%85%E6%96%B9%E6%B3%95%E3%82%92%E8%AA%BF%E6%9F%BB.md)

[INTERN-207 pangresのupdateの実装](https://github.com/PantaRhei-Developer/WIKI-PantaRhei/blob/main/WorkMemo/INTERN-207%20pangres%E3%81%AEupdate%E3%81%AE%E5%AE%9F%E8%A3%85.md)
  
