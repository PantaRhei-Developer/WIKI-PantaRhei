0. [結論](#結論)
1. [概要](#概要)
2. [ワークログ](#ワークログ)

# 0. 結論
json_to_sql.pyとmodify_json.pyをstart_scraping.shに組み込むことができた．

# 1. 概要
[INTERN-192: 開発したコードを週次バッチに組み込む完了](https://remotesalesproject.atlassian.net/browse/INTERN-192)
 

# 2. ワークログ
以下は週次スクレイピングを担う最終的なstart_scraping.shだ．

```
#!/bin/bash

# Set the PATH to include the directory where scrapy is installed
export PATH=$PATH:/home/kabaz7294/.local/bin

chmod +x ~/hellowork-scraping/hellowork-scraping/project/result

python3 modify_json.py

gsutil cp /home/kabaz7294/hellowork-scraping/hellowork-scraping/project/result/* gs://hellowork-bucket/scraping-log/
rm -rf /home/kabaz7294/hellowork-scraping/hellowork-scraping/project/result/*

python3 json_to_sql.py

start_scraping_time=$(date '+%Y%m%d_%H%M')
cd /home/kabaz7294/hellowork-scraping/hellowork-scraping

# Specify the full path to scrapy
/home/kabaz7294/.local/bin/scrapy crawl hellowork -o /home/kabaz7294/hellowork-scraping/hellowork-scraping/project/result/result_${start_scraping_time}.json

cd /

sleep 5m
shutdown -h now

exit 0
```
