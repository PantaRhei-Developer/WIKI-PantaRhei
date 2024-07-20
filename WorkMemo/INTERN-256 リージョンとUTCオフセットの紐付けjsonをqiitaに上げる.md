# 目次

0. [結論](#結論)
1. [概要](#概要)
2. [ワークログ](#ワークログ)

# 0. 結論
UTC時間のオフセット（単位は時間）をGoogle Cloudのリージョン・ゾーンに紐づけました．

```
{
    "us-east1": {
      "us-east1-b": "-5",
      "us-east1-c": "-5",
      "us-east1-d": "-5"
    },
    "us-east4": {
      "us-east4-c": "-5",
      "us-east4-b": "-5",
      "us-east4-a": "-5"
    },
    "us-central1": {
      "us-central1-c": "-6",
      "us-central1-a": "-6",
      "us-central1-f": "-6",
      "us-central1-b": "-6"
    },
    "us-west1": {
      "us-west1-b": "-8",
      "us-west1-c": "-8",
      "us-west1-a": "-8"
    },
    "europe-west4": {
      "europe-west4-a": "+0",
      "europe-west4-b": "+0",
      "europe-west4-c": "+0"
    },
    "europe-west1": {
      "europe-west1-b": "+0",
      "europe-west1-d": "+0",
      "europe-west1-c": "+0"
    },
    "europe-west3": {
      "europe-west3-c": "+0",
      "europe-west3-a": "+0",
      "europe-west3-b": "+0"
    },
    "europe-west2": {
      "europe-west2-c": "+1",
      "europe-west2-b": "+1",
      "europe-west2-a": "+1"
    },
    "asia-east1": {
      "asia-east1-b": "+8",
      "asia-east1-a": "+8",
      "asia-east1-c": "+8"
    },
    "asia-southeast1": {
      "asia-southeast1-b": "+7",
      "asia-southeast1-a": "+7",
      "asia-southeast1-c": "+7"
    },
    "asia-northeast1": {
      "asia-northeast1-b": "+9",
      "asia-northeast1-c": "+9",
      "asia-northeast1-a": "+9"
    },
    "asia-south1": {
      "asia-south1-c": "+5.5",
      "asia-south1-b": "+5.5",
      "asia-south1-a": "+5.5"
    },
    "australia-southeast1": {
      "australia-southeast1-b": "+11",
      "australia-southeast1-c": "+11",
      "australia-southeast1-a": "+11"
    },
    "southamerica-east1": {
      "southamerica-east1-b": "-3",
      "southamerica-east1-c": "-3",
      "southamerica-east1-a": "-3"
    },
    "africa-south1": {
      "africa-south1-a": "+2",
      "africa-south1-b": "+2",
      "africa-south1-c": "+2"
    },
    "asia-east2": {
      "asia-east2-a": "+8",
      "asia-east2-b": "+8",
      "asia-east2-c": "+8"
    },
    "asia-northeast2": {
      "asia-northeast2-a": "+9",
      "asia-northeast2-b": "+9",
      "asia-northeast2-c": "+9"
    },
    "asia-northeast3": {
      "asia-northeast3-a": "+9",
      "asia-northeast3-b": "+9",
      "asia-northeast3-c": "+9"
    },
    "asia-south2": {
      "asia-south2-a": "+5.5",
      "asia-south2-b": "+5.5",
      "asia-south2-c": "+5.5"
    },
    "asia-southeast2": {
      "asia-southeast2-a": "+7",
      "asia-southeast2-b": "+7",
      "asia-southeast2-c": "+7"
    },
    "australia-southeast2": {
      "australia-southeast2-a": "+11",
      "australia-southeast2-b": "+11",
      "australia-southeast2-c": "+11"
    },
    "europe-central2": {
      "europe-central2-a": "+1",
      "europe-central2-b": "+1",
      "europe-central2-c": "+1"
    },
    "europe-north1": {
      "europe-north1-a": "+2",
      "europe-north1-b": "+2",
      "europe-north1-c": "+2"
    },
    "europe-southwest1": {
      "europe-southwest1-a": "+0",
      "europe-southwest1-b": "+0",
      "europe-southwest1-c": "+0"
    },
    "europe-west10": {
      "europe-west10-a": "+0",
      "europe-west10-b": "+0",
      "europe-west10-c": "+0"
    },
    "europe-west12": {
      "europe-west12-a": "+0",
      "europe-west12-b": "+0",
      "europe-west12-c": "+0"
    },
    "europe-west6": {
      "europe-west6-a": "+1",
      "europe-west6-b": "+1",
      "europe-west6-c": "+1"
    },
    "europe-west8": {
      "europe-west8-a": "+1",
      "europe-west8-b": "+1",
      "europe-west8-c": "+1"
    },
    "europe-west9": {
      "europe-west9-a": "+1",
      "europe-west9-b": "+1",
      "europe-west9-c": "+1"
    },
    "me-central1": {
      "me-central1-a": "+3",
      "me-central1-b": "+3",
      "me-central1-c": "+3"
    },
    "me-central2": {
      "me-central2-a": "+3",
      "me-central2-b": "+3",
      "me-central2-c": "+3"
    },
    "me-west1": {
      "me-west1-a": "+3",
      "me-west1-b": "+3",
      "me-west1-c": "+3"
    },
    "northamerica-northeast1": {
      "northamerica-northeast1-a": "-5",
      "northamerica-northeast1-b": "-5",
      "northamerica-northeast1-c": "-5"
    },
    "northamerica-northeast2": {
      "northamerica-northeast2-a": "-5",
      "northamerica-northeast2-b": "-5",
      "northamerica-northeast2-c": "-5"
    },
    "southamerica-west1": {
      "southamerica-west1-a": "-5",
      "southamerica-west1-b": "-5",
      "southamerica-west1-c": "-5"
    },
    "us-east5": {
      "us-east5-a": "-5",
      "us-east5-b": "-5",
      "us-east5-c": "-5"
    },
    "us-south1": {
      "us-south1-a": "-6",
      "us-south1-b": "-6",
      "us-south1-c": "-6"
    },
    "us-west2": {
      "us-west2-a": "-8",
      "us-west2-b": "-8",
      "us-west2-c": "-8"
    },
    "us-west3": {
      "us-west3-a": "-8",
      "us-west3-b": "-8",
      "us-west3-c": "-8"
    },
    "us-west4": {
      "us-west4-a": "-8",
      "us-west4-b": "-8",
      "us-west4-c": "-8"
    }
  }

```

# 1. 概要
[INTERN-256: リージョンとUTCオフセットの紐付けjsonをqiitaに上げる完了](https://remotesalesproject.atlassian.net/browse/INTERN-256)
 

# 2. ワークログ
qiitaに投稿しました．

[Google Cloudのリージョン・ゾーンとUTC時間のオフセット(単位:時間)を紐づけました！！！ - Qiita ](https://qiita.com/haruki_pantarhei/items/e606515ef04c092796d9)

