# leadknock チュートリアル

## はじめに
leadknockの開発手順のなぐり書き．</br>
のちのち手を加えていく

## 目次
- [leadknock チュートリアル](#leadknock-チュートリアル)
  - [はじめに](#はじめに)
  - [目次](#目次)
  - [環境設定](#環境設定)
    - [前提](#前提)
    - [フロントエンド](#フロントエンド)
    - [バックエンド](#バックエンド)
  - [ディレクトリ構造(省いているファイルあり)](#ディレクトリ構造省いているファイルあり)
    - [1層目のディレクトリ構成](#1層目のディレクトリ構成)
    - [todo](#todo)
  - [とりあえず](#とりあえず)
    - [リファクタするときに参考にするコード](#リファクタするときに参考にするコード)
  - [デプロイ](#デプロイ)

## 環境設定

### 前提
- **GitHubにssh接続ができる**
- **Node.js 16.xがインストールされている**
- **Dockerがインストールされている**

### フロントエンド
```
$ git clone -b develop git@github.com:PantaRhei-Developer/leadknock-frontend.git
$ cd leadknock-frontend
```
nuxt.config.jsのコードを一部改変
```diff
# 61行目
- baseURL: "https://leadknock-backend-dw4fpp232q-an.a.run.app",
+ baseURL: "http://localhost:8000",

# 93行目
- url: "https://leadknock-backend-dw4fpp232q-an.a.run.app",
+ url: "http://localhost:8000",
```
```
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev
```

### バックエンド
.envとkey.jsonをファイル管理者から受け取った状態で下記の動作を実行してください．
```
$ git clone -b develop git@github.com:PantaRhei-Developer/leadknock-backend.git
$ cd leadknock-backend

# docker環境構築
$ docker compose run --entrypoint "poetry install --no-root" leadknock-api
$ docker compose build --no-cache

# コンテナ立ち上げ
$ docker compose up
```

## ディレクトリ構造(省いているファイルあり)
### 1層目のディレクトリ構成
```
leadknock-backend
├ .dockervenv/
├ .venv/
├ api/
├ .env
├ .gitignore
├ cloudbuild.yaml
├ docker-compose.yaml
├ Dockerfile
├ key.json
└ .gitignore
```

| TH | TH |
| ---- | ---- |
| TD | TD |
| TD | TD |

### todo
- 他の階層を書く
- 表に主要なファイルの説明を書く

## とりあえず
### リファクタするときに参考にするコード
1. repはleadknockでbranchはtransferを見ましょう</br>
   https://github.com/PantaRhei-Developer/leadknock/tree/transfer
2. 実装するapiはurls.pyを見ましょう</br>
   https://github.com/PantaRhei-Developer/leadknock/blob/transfer/dashboard/app/urls.py</br>
   実装する際，pathの先頭がapiになっているか，.as_view()の前がAPIViewになっているものを実装しましょう．
   ```
   # example
   # ☓
   path('dashboard/saleslog',
        DashboardSalesLogView.as_view(), name="dashboard_saleslog"),
   # ◯
   path('api/dashboard/saleslog',
        DashboardSalesLogAPIView.as_view(), name="api_dashboard_saleslog"),
   ```
3. 実装するapiが決まったらimportされているファイルを見に行きましょう</br>
   ```
   # example
   from .views import (ProjectListView
                        ...
                        DashboardSalesLogAPIView,
                        ...
                        ImportDataApiView)

   path('api/dashboard/saleslog',
        DashboardSalesLogAPIView.as_view(), name="api_dashboard_saleslog"),
   ```
   views.pyにあることがわかりました．
4. views.pyを見てコードを実装しましょう

## デプロイ
下記の図のdev環境まで完成しています．</br>
開発者はプルリクを出してマージされると勝手にCloud Runにデプロイされます．</br>
すごく便利！
![arch](https://github.com/PantaRhei-Developer/WIKI-PantaRhei/assets/147671633/a58aee43-d1d4-42a0-8201-d39686f471b5)
