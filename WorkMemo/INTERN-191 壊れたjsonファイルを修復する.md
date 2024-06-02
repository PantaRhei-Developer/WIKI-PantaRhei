# 目次

0. [結論](#結論)
1. [概要](#概要)
2. [ワークログ](#ワークログ)
    - [Pythonのjsonライブラリ](#pythonのjsonライブラリ)
    - [rstripを使用](#rstripを使用)

# 0. 結論
modify_json.pyとmodify_json_at_gcs.pyを開発した．

# 1. 概要
[INTERN-191: 壊れたjsonファイルを修復する完了](https://remotesalesproject.atlassian.net/browse/INTERN-191)
 
scrapyのスクレイピングがfinishedせず，何らかの理由で中断される時がある．中断されたスクレイピングの結果は不完全なjsonファイルに保管される．具体的には，”]”で終わるはずが，”,”で終了してしまう．

![alt text](../images/image116.png)

これは，scrapyの仕様だ．scrapyはスクレイピングの結果を一行ずつjsonファイルに書き込み，末尾を",改行“にする．

正常にfinishedした場合は"]“で閉じられ，完全なjsonが作成される．

本チケットでは，正常に終了しなかったjsonファイルを完全なファイルに修復することを扱う．

# 2. ワークログ
## 2.0. Pythonのjsonライブラリ
Pythonのjsonライブラリは不完全なjsonファイルを扱うことができないため，今回の実装には不向きだ．

## 2.1. rstripを仕様
rstripを使用し，jsonライブラリの代用が叶った．

以下が，"]“で閉じられていないjsonファイルを部分修正し，完全なものにするmodify_json.pyだ．
```
import os

def fix_json_file(file_path):
    with open(file_path, 'r', encoding='utf-8') as f:
        data = f.read()
    
    if data.endswith(',\n'):
        # カンマの修正
        data = data.rstrip(',\n') + '\n]'
        with open(file_path, 'w', encoding='utf-8') as f:
            f.write(data)

def fix_all_json_files(directory):
    for filename in os.listdir(directory):
        if filename.endswith(".json"):
            json_file_path = os.path.join(directory, filename)
            fix_json_file(json_file_path)

directory_path = '/home/kabaz7294/hellowork-scraping/hellowork-scraping/project/result/'
fix_all_json_files(directory_path)
```

また，GCS上の不完全なjsonファイルを"]“で閉じられた完全なファイルにして上書きするコードを開発した．↓modify_json_at_gcs.py

```
import os
import json
from google.cloud import storage

def fix_json_file(bucket_name, file_name):
    client = storage.Client()
    bucket = client.get_bucket(bucket_name)
    blob = bucket.blob(file_name)

    # ファイルのダウンロード
    data = blob.download_as_text()

    if data.endswith(',\n'):
        # カンマの修正
        data = data.rstrip(',\n') + '\n]'

        # 修正したデータをアップロード
        blob.upload_from_string(data, content_type='application/json')

def fix_all_json_files(bucket_name, folder_path):
    client = storage.Client()
    bucket = client.get_bucket(bucket_name)

    # フォルダ内のすべてのファイルを処理
    blobs = bucket.list_blobs(prefix=folder_path)
    for blob in blobs:
        if blob.name.endswith(".json"):
            fix_json_file(bucket_name, blob.name)

# Google Cloud Storageのバケット名とフォルダパス
bucket_name = 'hellowork-bucket'
folder_path = 'scraping-log/'

fix_all_json_files(bucket_name, folder_path)
```
