# 目次

1. [結論](#結論)
2. [概要](#概要)
3. [ワークログ](#ワークログ)
   - [pangresのインストール](#pangresのインストール)
   - [pd.to_sqlのかわりにpangres.upsert](#pd.to_sqlのかわりにpangres.upsert)
     - [解決策](#解決策)
   - [All index levels must be named!](#All-index-levels-must-be-named!)
     - [解決策](#解決策)


# 0. 結論
pangresを使用し，jsonのデータをUpsertするように，json_to_sql.pyを変更した．

```
import pandas as pd
from sqlalchemy import create_engine
from sqlalchemy.dialects.postgresql import HSTORE
import json
import re
from google.cloud import storage
from pangres import upsert

with open('info.json', 'r', encoding='utf-8') as f:
    info = json.load(f)

def get_recently_log_filename():
    bucket_name = info['bucket_name']
    log_folder = info['log_folder']

    client = storage.Client()

    # バケットのlog取得
    bucket = client.get_bucket(bucket_name)
    blobs = bucket.list_blobs(prefix=log_folder)

    max_value = -1
    max_file_name = ""

    # オブジェクト一覧からファイル名を取得
    for blob in blobs:
        file_name = blob.name
        # 指定されたパターンに一致するかチェック
        match = re.match(r'^scraping-log/result_(\d{8})_(\d{4})\.json$', file_name)

        if match:
            x, y = map(int, match.groups())

            concatenated_value = int(f'{x:08d}{y:04d}')

            if concatenated_value > max_value:
                max_value = concatenated_value
                max_file_name = file_name
    return max_file_name


# 接続情報
db_user = info['db_user']
db_password = info['db_password']
db_name = info['db_name']
db_instance_ip = info['db_instance_ip']

bucket_name = info['bucket_name']
table_name = info['table_name']

json_file_name = get_recently_log_filename()

# Google Cloud Storageからデータを読み込む
json_file_path = f'gs://{bucket_name}/{json_file_name}'

df = pd.read_json(json_file_path, encoding='utf-8', orient='records')
df.set_index(["company_location", "job_content", "job_annual_income", "job_start_date", "job_end_date"], inplace=True)

# SQLAlchemy Engineの作成
engine = create_engine(f'postgresql+psycopg2://{db_user}:{db_password}@{db_instance_ip}/{db_name}', echo=True)

upsert(con=engine, df=df, schema='public', table_name=table_name, if_row_exists='update', create_table=False, chunksize=5000,
       dtype={'job_application_steps': HSTORE, 'job_application_contact_info': HSTORE, 'company_recruit_responsible': HSTORE})
```

# 1. 概要
[INTERN-207: pangresのupdateの実装完了](https://remotesalesproject.atlassian.net/browse/INTERN-207)

# 2. ワークログ
## 2.0. pangresのインストール

```
pip install pangres
```

## 2.1. pd.to_sqlのかわりにpangres.upsert
pangres.upsertを使用すれば，DataFrameをそのままデータベースのテーブルへUpsertできるようだ．

[DataframeをそのままPostgresにUPSERTできちゃうPangres | ShimacoTrip ](https://shimacotrip.com/dataframe%E3%82%92%E3%81%9D%E3%81%AE%E3%81%BE%E3%81%BEpostgres%E3%81%ABupsert%E3%81%A7%E3%81%8D%E3%81%A1%E3%82%83%E3%81%86pangres/)

```
upsert(engine=engine,
          df=df,
          schema=schema,
          table_name=table_name,
          ......
```

上のサイトを参考に，コードを書いてみるが，pangres.upsertの引数”engine”が存在しないというエラーが出た．どうやらこのサイトはいい加減か，古いバージョンのpangresを使用しているようだ．

**解決策**

[Upsert](https://github.com/ThibTrip/pangres/wiki/upsert)

pangresのドキュメントからUpsertの正式な引数名を見つけた．これを元に，upsertを実装した．

```
upsert(con=engine, df=df, schema='public', table_name=table_name, if_row_exists='update', create_table=False, chunksize=5000,
       dtype={'job_application_steps': HSTORE, 'job_application_contact_info': HSTORE, 'company_recruit_responsible': HSTORE})
```

dtypeがあってよかったｗ
もし無かったら，dict型のエラーと退治しなくてはならなかったところだった．

## 2.2. All index levels mustbe named!
実行してみると，以下のエラーが出てきた．
```
pangres.exceptions.UnnamedIndexLevelsException: All index levels must be named!
```

**解決策**

indexにも名前がついていなければいけないようだ．DataFrameのindexはテーブルに挿入することはないので，indexに名前を付ける代わりに，複合主キーをindexに変更した．

```
df.set_index(["company_location", "job_content", "job_annual_income", "job_start_date", "job_end_date"], inplace=True)
```

結果，エラーは解消した．
