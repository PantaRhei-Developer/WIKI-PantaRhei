# 目次

0. [結論](#結論)
1. [概要](#概要)
2. [ワークログ](#ワークログ)
3. [その他](#その他)

# 0. 結論
2024年4月13日現在，GitHubにあるコードについてまとめた．

# 1. 概要
[INTERN-346: GitHubにあるスクレイピングコードの媒体についてまとめるレビュー中](https://remotesalesproject.atlassian.net/browse/INTERN-346)

2024年4月12日にスクレイピング関係のリポジトリを1つにまとめることが決定された．1つにまとめる際，スクレイピングのコードの書き方を統一することを目指したい．まずは，2024年4月13日現状で，GitHubにどの媒体のスクレイピングコードが有るのか，また，それらは誰が作っているのか調査する．

# 2. ワークログ
現状存在するスクレイピングコードは以下のとおりだ

| リポジトリ名 | スクレイピング先のサービス名 | スクレイピング先のURL | 担当者 | 更新日 |
|--------------|----------------------------|-----------------------|--------|--------|
| [mynavi-shinsotsu-scraping](https://github.com/PantaRhei-Developer/mynavi-shinsotsu-scraping) | マイナビ新卒 | [マイナビ - 学生向け就職活動（就活）・就職情報サイト](https://job.mynavi.jp/) | manhtheinfitech, KazuTanaka | 2 years ago |
| [mynavi2023](https://github.com/PantaRhei-Developer/mynavi2023) | マイナビ新卒 | [マイナビ - 学生向け就職活動（就活）・就職情報サイト](https://job.mynavi.jp/) | KazuTanaka, realmadridmarcelo | 2 years ago |
| [RikunabiNEXT](https://github.com/PantaRhei-Developer/RikunabiNEXT) | リクナビNEXT | [https://next.rikunabi.com/](https://next.rikunabi.com/) | KazuTanaka, nguyendinhmanh11k58, ThangDao0611 | 2 years ago |
| [mynavi-tenshoku-scraping](https://github.com/PantaRhei-Developer/mynavi-tenshoku-scraping) | マイナビ転職 | [新着求人情報 マイナビ転職 ](https://tenshoku.mynavi.jp/newjob/)| realmadridmarcelo, hatsu989385, KazuTanaka, manhtheinfitech | last week |
| [hellowork-scraping](https://github.com/PantaRhei-Developer/hellowork-scraping) | ハローワーク | [ハローワークインターネットサービス - トップページ](https://www.hellowork.mhlw.go.jp/) | realmadridmarcelo, nguyendinhmanh11k58, pantarhei-haruki, manhtheinfitech | 3 months ago |
| [jobj](https://github.com/PantaRhei-Developer/jobj) | 求人ジャーナルネット | [アルバイト・派遣・転職・正社員の求人情報が満載！ - 求人ジャーナル](https://www.job-j.net/) | manhtheinfitech | 2 years ago |
| [townwork](https://github.com/PantaRhei-Developer/townwork) | タウンワーク | [https://townwork.net](https://townwork.net) | manhtheinfitech | 2 years ago |
| [baitoru](https://github.com/PantaRhei-Developer/baitoru) | バイトル | [【バイトル】でバイト選び！アルバイト・パートの求人・仕事探しならバイトル](https://www.baitoru.com/) | ThangDao0611 | 2 years ago |
| [e-aidem](https://github.com/PantaRhei-Developer/e-aidem) | イーアイデム | [アルバイト・バイト・パートの求人情報ならイーアイデム](https://www.e-aidem.com/) | realmadridmarcelo, manhtheinfitech | 2 years ago |
| [yahoo-finance](https://github.com/PantaRhei-Developer/yahoo-finance) | ヤフーファイナンス | [日本株 - Yahoo!ファイナンス](https://finance.yahoo.co.jp/stocks/) | KazuTanaka, nguyendinhmanh11k58, lam612 | 2 years ago |
| [type-scraping](https://github.com/PantaRhei-Developer/type-scraping) | type | [求人検索結果一覧－転職ならtype](https://type.jp/job/search.do) | realmadridmarcelo, KazuTanaka, manhtheinfitech, ThangDao0611 | 2 years ago |
| [JapanPensionService](https://github.com/PantaRhei-Developer/JapanPensionService) | 日本年金機構 | [https://www.nenkin.go.jp/index.html](https://www.nenkin.go.jp/index.html) | KazuTanaka, ThangDao0611 | 2 years ago |
| [shufu-job-scraping](https://github.com/PantaRhei-Developer/shufu-job-scraping) | しゅふJOB | [しゅふＪＯＢ｜しゅふに嬉しい求人が見つかる](https://part.shufu-job.jp/) | realmadridmarcelo, toto-inu, ThangDao0611 | 2 years ago |
| [job-terminal-scraping](https://github.com/PantaRhei-Developer/job-terminal-scraping) | Create転職 | [転職ならクリエイト転職-求人・転職情報サイト](https://www.job-terminal.com/) | realmadridmarcelo, ThangDao0611, kuwana, manhtheinfitech | 2 years ago |
| [arbeit-jungle-scraping](https://github.com/PantaRhei-Developer/arbeit-jungle-scraping) | Createバイト | [クリエイトバイト-パート求人の仕事探し・バイト探し](https://www.arbeit-jungle.com/) | realmadridmarcelo, ThangDao0611, KazuTanaka | 2 years ago |
| [workport](https://github.com/PantaRhei-Developer/workport) | WORKPORT | [転職エージェント｜無料転職相談のワークポート](https://www.workport.co.jp/) | realmadridmarcelo, toto-inu, ThangDao0611 | 2 years ago |
| [en-tenshoku](https://github.com/PantaRhei-Developer/en-tenshoku) | エン転職 | [転職なら【エン転職】 日本最大級の転職サイト](https://employment.en-japan.com/) | realmadridmarcelo, manhtheinfitech, ThangDao0611 | 2 years ago |
| [j-sen-scraping](https://github.com/PantaRhei-Developer/j-sen-scraping) | マッハバイト | [【最大１万円のマッハボーナス】マッハバイトでバイト探し](https://employment.en-japan.com/) | realmadridmarcelo, huytheinfitech, kuwana | 2 years ago |
| [from-a-scraping](https://github.com/PantaRhei-Developer/from-a-scraping) | From A navi | [＜毎日更新＞関東のバイト・アルバイト求人情報【フロムエー】｜パートの仕事も満載](https://www.froma.com/P01/) | manhtheinfitech, KazuTanaka, TangDao0611, huyrua291996, Trong Xuyen, Trong Xuyen, ntxuyen1989, realmadridmarcelo | 2 years ago |
| [fromA-scraping](https://github.com/PantaRhei-Developer/fromA-scraping) | From A navi | [＜毎日更新＞関東のバイト・アルバイト求人情報【フロムエー】｜パートの仕事も満載](https://www.froma.com/P01/) | yuyanakai128, realmadridmarcelo | 2 years ago |
| [mynavi-baito](https://github.com/PantaRhei-Developer/mynavi-baito) | マイナビバイト | [★マイナビバイト★でバイト・アルバイトの求人・仕事探し！｜Web応募もOK](https://baito.mynavi.jp/) | KazuTanaka, huyrua291996 | 2 years ago |
| [doda-scraping](https://github.com/PantaRhei-Developer/doda-scraping) | doda | [転職ならdoda(デューダ) 求人､転職情報満載の転職サイト](https://doda.jp/) | realmadridmarcelo, manhtheinfitech, ThangDao0611, ThangDao0611 | 2 years ago |
| [rikunabi-shinsotsu2023](https://github.com/PantaRhei-Developer/rikunabi-shinsotsu2023) | リクナビ新卒 | [【就活ならリクナビ】新卒・既卒の就職活動・採用情報サイト](https://job.rikunabi.com/) | KazuTanaka | 2 years ago |
| [create-arbeit-scraping](https://github.com/PantaRhei-Developer/create-arbeit-scraping) | Createバイト | [クリエイトバイト-パート求人の仕事探し・バイト探し](https://www.arbeit-jungle.com/) | takeo-fujiwara-72o, realmadridmarcelo | 2 years ago |
| [Nikkei-scraping](https://github.com/PantaRhei-Developer/Nikkei-scraping) | 日本経済新聞 | [日経会社情報DIGITAL : 日経電子版](https://www.nikkei.com/nkd/) | realmadridmarcelo, CodeCoaching | 2 years ago |
| [hp_crawl](https://github.com/PantaRhei-Developer/hp_crawl) |  |  | KazuTanaka | 2 years ago |
| [Fuma_scraping](https://github.com/PantaRhei-Developer/Fuma_scraping) | FUMA | [https://fumadata.com/](https://fumadata.com/) | realmadridmarcelo | 2 years ago |

[スクレイピングに関するリポジトリ調査.xlsx](https://github.com/user-attachments/files/15524473/default.xlsx)


# 3. その他
[panta-workspace](https://github.com/PantaRhei-Developer/panta-workspace)

GitHubにDocker関係のリポジトリがあった．


