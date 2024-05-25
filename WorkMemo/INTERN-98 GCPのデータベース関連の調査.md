*   1 [0. 結論](#0.結論)
*   2 [1. 概要](#1.概要)
*   3 [2. 参考](#2.参考)
*   4 [3. データベースプロダクト比較](#3.データベースプロダクト比較)
*   5 [4. クエリ言語がSQLのプロダクトの場合どれがいいか](#4.クエリ言語がSQLのプロダクトの場合どれがいいか)
    *   5-1 [4-1. クエリ言語がSQLのプロダクトの比較](#4-1.クエリ言語がSQLのプロダクトの比較)
*   6 [5. ストレージ選択早見表](#5.ストレージ選択早見表)
*   7 [6. Cloud SQLとCloud Spannerの詳細比較](#6.CloudSQLとCloudSpannerの詳細比較)
    *   7-1 [6-1. 比較表](#6-1.比較表)
    *   7-2 [6-2. 使用料金](#6-2.使用料金)
*   8 [7. メモ](#7.メモ)
    *   7-1 [7-1. 水平スケール](#7-1.水平スケール)

# 0. 結論
Cloud SQLかCloud Spannerよさそう

・グローバル水平スケールが求められる → Spanner

・大量データ(64TB以上)を扱う → Spanner

・上記に当てはまらない → Cloud SQL

# 1. 概要
[INTERN-98: GCPのデータベース関連の調査完了](https://pantarhei-hub.atlassian.net/browse/INTERN-98)
 
GCPのデータベースプロダクトの比較

# 2. 参考
https://note.com/thanab/n/nee2656c8f3a9
https://cloud-ace.jp/column/detail423/
https://qiita.com/k_0120/items/e461505efd0eb03886f2
https://www.topgate.co.jp/blog/techblog/19534

# 3. データベースプロダクト比較
1.プロダクト名:

  ・Cloud Spanner

  ・Cloud Firestore

  ・Cloud Bigtable

  ・Cloud SQL

  ・Cloud BigQuery

2.データモデル:

  ・Cloud Spanner: リレーショナル

  ・Cloud Firestore: ドキュメント指向

  ・Cloud Bigtable: ワイドカラムストア

  ・Cloud SQL: リレーショナル

  ・Cloud BigQuery: 列指向（シェマレス）

3.スケーラビリティ:

  ・Cloud Spanner: グローバルな水平スケーリング

  ・Cloud Firestore: 自動シャーディングによるスケーリング

  ・Cloud Bigtable: 高い水平スケーリング

  ・Cloud SQL: 垂直および水平スケーリング

  ・Cloud BigQuery: 高い水平スケーリング

4.クエリ言語:

  ・Cloud Spanner: SQL

  ・Cloud Firestore: NoSQLクエリ

  ・Cloud Bigtable: 列指向クエリ言語

  ・Cloud SQL: SQL

  ・Cloud BigQuery: SQL

5.トランザクション:

  ・Cloud Spanner: 分散トランザクション

  ・Cloud Firestore: トランザクションサポートあり

  ・Cloud Bigtable: トランザクションサポートなし

  ・Cloud SQL: トランザクションサポートあり

  ・Cloud BigQuery: トランザクションサポートなし

6.データの整合性:

  ・Cloud Spanner: 一貫性（外部一貫性）

  ・Cloud Firestore: 一貫性（外部一貫性）

  ・Cloud Bigtable: 最終整合性

  ・Cloud SQL: 一貫性

  ・Cloud BigQuery: 最終整合性

7.データのバックアップと復元:

  ・Cloud Spanner: 自動バックアップ

  ・Cloud Firestore: 自動バックアップ

  ・Cloud Bigtable: ユーザー管理型バックアップ

  ・Cloud SQL: ユーザー管理型バックアップ

  ・Cloud BigQuery: ユーザー管理型バックアップ

8.価格モデル:

  ・Cloud Spanner: プロビジョニングおよび従量制

  ・Cloud Firestore: 従量制

  ・Cloud Bigtable: 従量制

  ・Cloud SQL: 従量制

  ・Cloud BigQuery: 従量制

9.使用ケース:

  ・Cloud Spanner: トランザクショナルなアプリケーション、グローバルなアプリケーション

  ・Cloud Firestore: ドキュメント指向のアプリケーション

  ・Cloud Bigtable: 大規模な分散データ、時系列データ

  ・Cloud SQL: 一般的なリレーショナルデータベースの使用ケース

  ・Cloud BigQuery: ビッグデータ分析、データウェアハウス

4. クエリ言語がSQLのプロダクトの場合どれがいいか
読みの早さ重視

・データ分析は考慮しない

・レスポンスが速いほうがいい

・料金は少なくしたい

上記を考慮してgptくんに聞いてみた↓

Google Cloud SQL for PostgreSQLは、読みの速さやPostgreSQLの使用、料金の最適化に適している場合があります。また、Managed Serviceとして提供されており、インフラストラクチャの管理に手間をかけずに、高いレスポンス速度を維持できる可能性があります。

ただし、具体的なプロジェクトの要件やトラフィックなどにより最適なプロダクトが変わる可能性があります。特に、将来的な成長や追加の要件を考慮しても良い選択を行うことが重要です。


## クエリ言語がSQLのプロダクトの比較
1.	**Cloud SQL (PostgreSQL) vs. Cloud Spanner:**

・**読みの速さ**: Cloud Spannerはグローバルな分散トランザクションデータベースであり、読み込み性能が高いですが、Cloud SQLも高性能であり、PostgreSQLエンジンを使用することで高速な読み込みが期待できます。

・**データ分析不要**: Cloud Spannerはデータ分析にも使えますが、Cloud SQLが主にトランザクション処理向けなので、データ分析が不要な場合、Cloud SQLの方がシンプルかつコスト効果的かもしれません。

2.**Cloud SQL (PostgreSQL) vs. Cloud Bigtable:**

・**読みの速さ**: Cloud Bigtableは大規模な分散データ向けであり、読み込み性能が高いですが、データモデルが異なるため、使用するデータによります。Cloud SQLはリレーショナルデータに向いています。

・**データ分析不要**: Cloud Bigtableは時系列データや大規模なデータ向けであり、トランザクショナルなデータ処理には向いていません。Cloud SQLはその点で適しています。

3.**Cloud SQL (PostgreSQL) vs. Cloud BigQuery:**

・**読みの速さ**: Cloud BigQueryは大規模なデータセットに対する分析が得意ですが、Cloud SQLがトランザクション処理向けであるため、読み込み性能ではCloud SQLが有利となることがあります。

・**データ分析不要**: Cloud BigQueryは主にデータ分析やビッグデータウェアハウス向けです。Cloud SQLはトランザクション処理が主体です。

# 5. ストレージ選択早見表
![alt text](../images/image2５.png)

参考：https://qiita.com/k_0120/items/e461505efd0eb03886f2

Cloud Datastoreも良さそうだけどNoSQLみたい

Cloud SQLかCloud Spannerがよさそう

# 6. Cloud SQLとCloud Spannerの詳細比較

## 比較表
| 項目 | Spanner | Cloud SQL |
| ---- | ------- | --------- |
| 顧客管理の暗号鍵（CMEK） | OK | OK |
| SLO（稼働率） | - マルチリージョン: >= 99.999%<br>- リージョン: >= 99.99% | >= 99.95% |
| レプリケーション | - 読み書きレプリカ<br>- 読み取り専用レプリカ<br>- ウィットネスレプリカ | - リードレプリカ |
| テーブル間の関係定義 | インターリーブ、外部キー | 外部キー |
| ストレージ上限 | 1ノードあたり2TB | 最大 64 TB まで。マシンタイプによって異なる。 |

## 使用料金
Spanner の料金は主に、ノード数 + ストレージ量

Cloud SQL の料金は主に、インスタンス性能 + ストレージ量

で算出される。

# 7.メモ

## 水平スケール

→台数を増やすことで全体の性能を上げる

適した利用方法

・大規模なシステムを運用する

・突発的なアクセス増加に対応する

 
