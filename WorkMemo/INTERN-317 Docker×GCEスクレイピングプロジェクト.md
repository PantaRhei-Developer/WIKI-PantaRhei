0. [ゴール](#ゴール)
1. [概要](#概要)
   - [背景](#背景)
   - [道筋](#道筋)
   - [メモ](#メモ)
2. [ワークログ](#ワークログ)

# 0. ゴール
dockerコンテナ with helloworkのスクレイピングプロジェクトがgceにあがっている状態 かつ アーキテクチャ図が完成している状態．

# 1. 概要
[INTERN-317: Docker×GCEスクレイピングプロジェクトBACKLOG](https://remotesalesproject.atlassian.net/browse/INTERN-317[)
 

## ■背景
GKEやCloud Runを利用したコンテナ運用について調査したが，コンテナごとにIPアドレスを紐づけることをきれいな実装をすることは難しそうである．Cloud Runではプロキシサーバを使用しなければならない．GKEではパッドとコンテナを１対１対応させる必要がある．

そこで，GCEにコンテナを配置する運用に着手する．

## ■道筋
dockerを勉強（さくらインターネット）

dockerファイル・イメージを作成

docker×gceの勉強

３の調査で問題がなければ，コンテナがgceに上がっている状態にする

スクレイピングのアーキテクチャ

============このエピックではこの上までを扱う====================

CI/CDを考えた運用を調査（岸本さんと一緒に考える）

dockerファイルをgceにいれる

ポートやネットワークの問題が発生する

## ■メモ
url，xpath，itemsなど，最低限のコードを変えることで，別媒体に適用したdockerファイルにしてスクレイピングをできるようにする．その際，最低限のコードが何かをまとめておく．

ベトナムの会社が作成したものを参考にする

pip install -r requirements.txt

# 2. ワークログ
[INTERN-323 DockerのインストールとVSCでのセットアップ](https://github.com/PantaRhei-Developer/WIKI-PantaRhei/blob/main/WorkMemo/INTERN-323%20Docker%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB%E3%81%A8VSC%E3%81%A7%E3%81%AE%E3%82%BB%E3%83%83%E3%83%88%E3%82%A2%E3%83%83%E3%83%97%20%20.md)

[INTERN-346 GitHubにあるスクレイピングコードの媒体についてまとめる](https://github.com/PantaRhei-Developer/WIKI-PantaRhei/blob/main/WorkMemo/INTERN-346%20GitHub%E3%81%AB%E3%81%82%E3%82%8B%E3%82%B9%E3%82%AF%E3%83%AC%E3%82%A4%E3%83%94%E3%83%B3%E3%82%B0%E3%82%B3%E3%83%BC%E3%83%89%E3%81%AE%E5%AA%92%E4%BD%93%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6%E3%81%BE%E3%81%A8%E3%82%81%E3%82%8B.md)

[INTERN-318 Dockerの勉強](https://github.com/PantaRhei-Developer/WIKI-PantaRhei/blob/main/WorkMemo/INTERN-318%20Docker%E3%81%AE%E5%8B%89%E5%BC%B7.md)
