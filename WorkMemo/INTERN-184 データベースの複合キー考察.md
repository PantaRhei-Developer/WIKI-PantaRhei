0. [結論](#結論)
1. [概要](#概要)
2. [ワークログ](#ワークログ)

# 0. ゴール
helloworkのscrapingデータを入れるテーブルに置ける複合キーを決める．

複合キー：会社と求人の両方とも区別できる列の組み合わせを主キーとしたもの

■問題
・会社を決めるためのキーは何を採用するか．会社名や会社の住所が良さそうだが，欠損がある．どんなデータに欠損があるのか調査する．

・仕事内容（job_content）と給料とjob_start_date，job_end_dateの４つを求人を区別する複合キーとする．しかし，仕事内容はGCSに入れる予定だったため，scrapyコードを変更する必要がある．

■やること
・GCSに入れるカラムもスクレイピングするようにscrapyを改良する．
・会社情報を欠損させる企業にはどのようなものがあるのか分析する．

# 1. 概要
[INTERN-184: データベースの複合キー考察完了](https://remotesalesproject.atlassian.net/browse/INTERN-184)
 
# 2. ワークログ
[INTERN-183 helloworkのcompany_nameがつかない企業についての傾向を調査](https://github.com/PantaRhei-Developer/WIKI-PantaRhei/blob/main/WorkMemo/INTERN-183%20hellowork%E3%81%AEcompany_name%E3%81%8C%E3%81%A4%E3%81%8B%E3%81%AA%E3%81%84%E4%BC%81%E6%A5%AD%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6%E3%81%AE%E5%82%BE%E5%90%91%E3%82%92%E8%AA%BF%E6%9F%BB.md)
[INTERN-189 helloworkで新たに取得するデータのtag調査](https://github.com/PantaRhei-Developer/WIKI-PantaRhei/blob/main/WorkMemo/INTERN-189%20hellowork%E3%81%A7%E6%96%B0%E3%81%9F%E3%81%AB%E5%8F%96%E5%BE%97%E3%81%99%E3%82%8B%E3%83%87%E3%83%BC%E3%82%BF%E3%81%AEtag%E8%AA%BF%E6%9F%BB.md)
[INTERN-187 スクレイピングデータを入れるテーブルを作成](https://github.com/PantaRhei-Developer/WIKI-PantaRhei/blob/main/WorkMemo/INTERN-187%20%E3%82%B9%E3%82%AF%E3%83%AC%E3%82%A4%E3%83%94%E3%83%B3%E3%82%B0%E3%83%87%E3%83%BC%E3%82%BF%E3%82%92%E5%85%A5%E3%82%8C%E3%82%8B%E3%83%86%E3%83%BC%E3%83%96%E3%83%AB%E3%82%92%E4%BD%9C%E6%88%90.md)
  

