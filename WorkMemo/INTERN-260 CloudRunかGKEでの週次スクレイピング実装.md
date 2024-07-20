# 目次

1. [ゴール](#ゴール)
2. [概要](#概要)
3. [ワークログ](#ワークログ)

# 0. ゴール
Insertの実装を組み入れて，週次バッチ化成功させる．

# 1. 概要
[INTERN-260: CloudRunかGKEでの週次スクレイピング実装完了](https://remotesalesproject.atlassian.net/browse/INTERN-260)
 

GCEを今後複数の情報元からスクレイピングをする際，管理がしやすくなるためコンテナ化を目指す．

Google Cloudにはコンテナ化して管理するためのサービスが複数あるため，以下の点でどのサービスを利用するか調査し，helloworkでお試し実装する．

・週次バッチができるのか

・cloudSQLかcloud spanner

・週次バッチを1週間回すのに料金はどうか

# 2. ワークログ
[INTERN-240 Cloud Runもしくは，GKEで週次バッチスクレイピングが実装可能か調査](https://github.com/PantaRhei-Developer/WIKI-PantaRhei/blob/main/WorkMemo/INTERN-240%20Cloud%20Run%E3%82%82%E3%81%97%E3%81%8F%E3%81%AF%EF%BC%8CGKE%E3%81%A7%E9%80%B1%E6%AC%A1%E3%83%90%E3%83%83%E3%83%81%E3%82%B9%E3%82%AF%E3%83%AC%E3%82%A4%E3%83%94%E3%83%B3%E3%82%B0%E3%81%8C%E5%AE%9F%E8%A3%85%E5%8F%AF%E8%83%BD%E3%81%8B%E8%AA%BF%E6%9F%BB.md)
