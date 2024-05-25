*   1 [0. 結論](#0.結論)
*   2 [1. 概要](#1.概要)
*   3 [2. メモ](#2.メモ)

# 0. 結論
https://leadknock-front-dev-dot-leadknock-dev-403807.uw.r.appspot.com/ 
デプロイできた

# 1. 概要
[INTERN-89: leadnockのUIをGoogle App Engineにデプロイする完了](https://pantarhei-hub.atlassian.net/browse/INTERN-89)


# 2. メモ
GCPで`leadknock-dev`というプロジェクトを作成

1.`gcloud init`で初期化してプロジェクト選択

2.`gcloud app create --project=leadknock-dev-403807`
サーバはus-west1を選択

3.ビルドしてデプロイするためのファイルを書き出し
`yarn build`
`yarn generate`

4.デプロイ
`gcloud app deploy app.yaml --project leadknock-dev-403807`

5.閲覧
`gcloud app browse -s leadknock-front-dev`

でけた

