*   1 [0\. 結論](#0.-結論)
*   2 [1\. 概要](#1.-概要)
*   3 [2\. ワークログ](#2.-ワークログ)

# 0\. 結論

以下の問題点があると考えました。

1.  データ数が膨大で実行時間が長い
    
2.  14969428行のレコードがあるうち、company\_industryに値があるのは1083639行（約7％）
    
3.  corporate\_numberにはアルバイトの人数が含まれているのか不明
    
4.  `company_business_display`と`company_email`にはデータが入っていない
    
5.  company\_businessやcompany\_tagにはJavaScriptの改行や箇条書きの点が含まれている
    
6.  取得ミスのデータが未知数ある
    
7.  source\_job\_urlやsorce\_company\_urlには有効期限切れのURLが少なくない
    
8.  company\_industryの値の型は共通していない
    
9.  company\_industryの値は複数あることもある
    
10.  宮川が意味を把握していないカラム名が多い
    

# 1\. 概要

[![](https://pantarhei-hub.atlassian.net/rest/api/2/universal_avatar/view/type/issuetype/avatar/10316)INTERN-48: ⓪データの理解Done](https://remotesalesproject.atlassian.net/browse/INTERN-48)

[Kaggleで勝つデータ分析の技術](https://gihyo.jp/book/2019/978-4-297-10843-4)

# 2\. ワークログ

今後開発は、対話型統合開発環境のJupyterLabでコーディングしようと考えています。理由は２つです。

①Jupyter Labでの操作に慣れていること

②JupyterLabはJupyter Notebookより若干使いやすいこと

[![](https://miyukimedaka.com/wp-content/uploads/2019/04/cropped-feesheeee-1-32x32.jpg)JupyterLabとJupyter Notebookの違いを簡単に解説【Mac】](https://miyukimedaka.com/2020/06/07/0143-jupyterlab-explanation/#toc5)

1.  データを読み取る
    

```Python
import numpy as np
import pandas as pd
df = pd.read_csv("dataterminal_20231009.csv")
df
```

これだけで約9分かかりました。カラム数が40あるとJupyter Labのデフォルトで真ん中のカラムが省略されて表示されます。以下のように設定することで省略をなくせました。

```
# 表示オプションを設定してすべての列を表示
pd.set_option('display.max_columns', None)
pd.set_option('display.expand_frame_repr', False)
```

2.  目的変数の欠損を確認する
    

表示されたdfの最初５行と最後５行には欠損値が多く見られました。特に目的変数が欠損値のレコードでは教師あり学習がかなわないため、以下のように目的変数に欠損がない状態のdataframeを作成しました。

```Python
df_dropna = df[df["company_industry"].notna()] df_dropna.head()
```

　dfの行数14969428行に対してdf\_dropnaの行数は1083639行でした。この結果から7％しか学習できるデータがないことが分かりましたが、実際のデータ分析で1083639行でうまくいくかどうかはやってみないとわからないと思います。

3.  他のカラムについても欠損状態を確認する
    

```Python
cols= df.columns
for c in cols:
    val_rate = df[df[c].notna()].shape[0] / df.shape[0]
print(f"{c}: {val_rate}")
```

実行時間38分でした。実行してから数値を丸めておけばよかったと後悔しつつも、この実行時間だとやり直しをする気力もなく、以下の実行結果で分析します。

```Python
###実行結果###
id: 1.0
source_job_url: 0.1293711423041682
source_company_url: 0.062113061367475096
corporate_number: 0.5641367859880818
job_start_date: 0.027012788999018534
job_end_date: 0.027012788999018534
company_recruit_tel: 0.046049588534712214
company_recruit_responsible: 0.04675262140944864
company_recruit_email: 0.00040716318619522405
company_address: 0.9813875987779894
company_average_age: 0.014036675282449002
company_business: 0.559142673988612
company_business_display: 0.0
company_capital: 0.1142422409192923
company_email: 0.0
company_employee: 0.5439163072897641
company_establish_year: 0.12810836860299538
company_fax: 0.09334478244592913
company_fiscal: 0.005903899601240608
company_hp_url: 0.0668084979599755
company_industry: 0.07239014075888538
company_name: 0.9956693068031724
company_city: 0.9819559571681696
company_area: 0.9801605645853669
company_name_eng_notation: 0.004728370382622502
company_name_kat_notation: 0.04830592057358504
company_postalcode: 0.5243657940704214
company_prefecture: 0.5592811562338922
company_representative: 0.12594963548373392
company_revenue: 0.015328174196101548
company_sect: 0.005161586668508643
company_sect_class: 0.0020979425533159983
company_sect_num: 0.004942673828285222
company_tag: 0.0055157752186656694
company_tel: 0.4138225588846815
process_flag: 1.0
info_source: 1.0
get_time: 1.0
created_at: 1.0
updated_at: 1.0
```

欠損でない割合が1％もないカラムがある。今後そのカラムのデータを増やす、または、カラムを削るか考慮する必要がありそうです。

4.  欠損がない場合どのようなデータが入っているのか
    

カラムごとに欠損していないデータを視覚化してみました。

```
cols = df.columns
for i in range(40):
    num = i
    df_col_dropna = df_dropna[df_dropna[cols[num]].notna()][cols[num]]
print(f"############{cols[i]}############")
print(df_col_dropna.head())
```

```Python
###実行結果###
############id############
54971
8320694
58122
8347421
82472
8132706
83302
8389350
115290
8125848
Name: id,
dtype: int64
############source_job_url############
54971
https://doda.jp/DodaFront/View/JobSearchDetail... 58122
https://doda.jp/DodaFront/View/JobSearchDetail... 82472
https://job.mynavi.jp/22/pc/search/corp209902/... 83302
https://doda.jp/DodaFront/View/JobSearchDetail... 115290
https://next.rikunabi.com/rnc/docs/cp_s01880.j... Name: source_job_url,
dtype: object
############source_company_url############
54971
https://doda.jp/DodaFront/View/Company/j_id__1... 82472
https://job.mynavi.jp/22/pc/search/corp209902/... 236253
https://doda.jp/DodaFront/View/Company/j_id__1... 236590
https://doda.jp/DodaFront/View/Company/j_id__1... 277875
https://doda.jp/DodaFront/View/Company/j_id__1... Name: source_company_url,
dtype: object
############corporate_number############
54971
8.010901e+12
58122
4.010701e+12
82472
3.240001e+12
83302
3.010701e+12
115290
2.410005e+12
Name: corporate_number,
dtype: float64
############job_start_date############
54971
2021/12/2
58122
2021/11/11
83302
2021/10/7
236253
2021/12/16
236590
2021/10/7
Name: job_start_date,
dtype: object
############job_end_date############
54971
2022/3/2
58122
2022/2/9
83302
2022/1/5
236253
2022/3/16
236590
2022/1/5
Name: job_end_date,
dtype: object
############company_recruit_tel############
280658
922822213.0
344959
436636188.0
366793
586769200.0
398395
791237837.0
422489
886788141.0
Name: company_recruit_tel,
dtype: float64
############company_recruit_responsible############
344959
代表取締役
366793
事務長
398395
採用担当者
422489
．
443777
院長夫人
Name: company_recruit_responsible,
dtype: object
############company_recruit_email############
6809395
recruit@realinvent.co.jp
6809762
vietnam-jp@rgf-hragent.asia
6809884
info@qsd.co.jp
6809932
jp.entry@reeracoen.co.id
6809951
ayane.sato@reeracoen.com.tw
Name: company_recruit_email,
dtype: object
############company_address############
54971
東京都世田谷区弦巻4丁目21-1
58122
東京都品川区東五反田2-20-4
NMF高輪ビル7F
83302
東京都品川区上大崎2-10-43
236253
香川県三豊市詫間町松崎2619-1
236590
東京都大田区西蒲田7-37-10グリーンプレイス蒲田ビル9F
Name: company_address,
dtype: object
############company_average_age############
236253 39.00 236590 37.20 334785 29.80 337510 34.10 338392 31.09 Name: company_average_age, dtype: float64
############company_business############
54971 きれいと元気のアンチエイジング専門店｢アエナ｣のチェーン展開アエナは健康食品・化粧品・美容雑... 82472 飲食事業部、業務用食品・酒類販売部、運送事業部、通販事業部,珈琲所　コメダ珈琲店の運営,台湾... 115290 幼保連携型認定こども園の運営 236253 ■事業内容：\n農・水・畜産物を主原料とした食品の製造販売 236590 ■事業内容 独自の「スケルカシステム」を用いた公共構造物の非破壊探査を通じて、社会インフラと... Name: company_business, dtype: object
############company_business_display############
Series([], Name: company_business_display, dtype: float64)
############company_capital############ 54971 5000.0 58122 2500.0 82472 1500.0 83302 379800.0 115290 0.0 Name: company_capital, dtype: float64
############company_email############
Series([], Name: company_email, dtype: float64)
############company_employee############
54971 77.0 58122 10.0 82472 50.0 83302 1356.0 115290 15.0 Name: company_employee, dtype: float64 ############company_establish_year############
54971 2004.0 58122 2018.0 83302 1918.0 115290 1957.0 236253 1975.0 Name: company_establish_year, dtype: float64
############company_fax############
344959 436636187.0 366793 586769222.0 422489 886687326.0 468121 427670851.0 1513197 878117737.0 Name: company_fax, dtype: float64
############company_fiscal############
1599947 2.0 2068071 2.0 2072743 3.0 2110979 9.0 2120060 3.0 Name: company_fiscal, dtype: float64 ############company_hp_url############
280658 http://www.runtec.co.jp/ 366793 https://hone-kenkou.com 468121 http://www.hirai-clinic.or.jp/ 1599947 https://www.jmf-reit.com/ 1899896 http://www.tenseikai.or.jp Name: company_hp_url, dtype: object
############company_industry############
54971 1011 58122 1022,2011 82472 2011,5014 83302 5021 115290 5024.0 Name: company_industry, dtype: object
############company_name############
54971 株式会社アエナ 58122 株式会社プラゴ 82472 ヒロボシ株式会社 83302 ホーチキ株式会社 115290 学校法人日景学園 Name: company_name, dtype: object
############company_city############
54971 世田谷区 58122 品川区 82472 広島市 83302 品川区 115290 大館市 Name: company_city, dtype: object
############company_area############
54971 弦巻4-21-1 58122 東五反田2-20-4 82472 西区商工センター2-16-17 83302 上大崎2-10-43 115290 釈迦内字館68-1 Name: company_area, dtype: object
############company_name_eng_notation############
1599947 Japan Metropolitan Fund Investment Corp. 2068071 Nishimatsuya Chain Co., Ltd. 2072743 Maruo Calcium Co., Ltd. 2110979 Azoom Co., Ltd. 2120060 Meito Sangyo Co., Ltd. Name: company_name_eng_notation, dtype: object
############company_name_kat_notation############
344959 カブシキガイシャ　リハビリノモリ 366793 イリョウホウジン　モンキーポッド　（モリセイケイゲカ） 398395 ヒトミクリニック（ガンカ） 422489 イリョウホウジン　トクシマオウシンクリニック 443777 イリョウホウジン　ハリマシカクリニック Name: company_name_kat_notation, dtype: object
############company_postalcode############
54971 154-0024 58122 141-0022 82472 733-0833 83302 141-0021 236253 769-1102 Name: company_postalcode, dtype: object
############company_prefecture############
54971 東京都 58122 東京都 82472 広島県 83302 東京都 115290 秋田県 Name: company_prefecture, dtype: object
############company_representative############
115290 理事長　日景　陽司 280658 代表取締役社長　山中　一裕 337510 代表取締役社長 貞方　宏司 344959 代表取締役　永島　徳之 366793 院長　松村　成毅 Name: company_representative, dtype: object
############company_revenue############
82472 2000.0 280658 54270.0 1272966 590.0 1272985 590.0 1273212 590.0 Name: company_revenue, dtype: float64
############company_sect############
337510 上場 377579 上場 418353 上場 1488544 上場 1534524 上場 Name: company_sect, dtype: object
############company_sect_class############
1599947 東証 2068071 東京証券取引所１部 2072743 東証２部 2110979 東証マザーズ 2120060 東京証券取引所１部 ,名古屋証券取引所１部 Name: company_sect_class, dtype: object
############company_sect_num############
1599947 89530.0 2068071 75450.0 2072743 41020.0 2110979 34960.0 2120060 22070.0 Name: company_sect_num, dtype: float64
############company_tag############
82472 \r\n\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t\t... 280658 中途入社5割以上,3年連続売上UP,産休・育休取得実績あり,育児中の社員在籍中 6809273 中途入社5割以上,3年連続売上UP,20代の管理職登用実績あり,育児中の社員在籍中 6809283 WEB面接OK,面接日程応相談,入社時期応相談,応募から内定まで1カ月以内 6809295 上場 Name: company_tag, dtype: object
############company_tel############
82472 822780130.0 1404588 342337415.0 1424719 643084427.0 1430111 362061608.0 1434793 364272020.0 Name: company_tel, dtype: float64
############process_flag############
54971 mapped 58122 mapped 82472 mapped 83302 mapped 115290 mapped Name: process_flag, dtype: object
############info_source############
54971 100001 58122 100001 82472 500000 83302 100001 115290 400000 Name: info_source, dtype: int64
############get_time############
54971 1.640544e+09 58122 1.640579e+09 82472 1.644944e+09 83302 1.640594e+09 115290 1.644944e+09 Name: get_time, dtype: float64
############created_at############
54971 2022-02-16 23:16:27.060664+09 58122 2022-02-16 23:15:52.274482+09 82472 2022-02-16 23:40:42.9629+09 83302 2022-02-16 23:17:46.744884+09 115290 2022-02-16 23:13:21.774908+09 Name: created_at, dtype: object
############updated_at############ 
4971 2022-02-16 23:16:27.060664+09 58122 2022-02-16 23:15:52.274482+09 82472 2022-02-16 23:40:42.9629+09 83302 2022-02-16 23:17:46.744884+09 115290 2022-02-16 23:13:21.774908+09 Name: updated_at, dtype: object
```

たまたま見つけてしまいましたが、実行結果の55行目は取得にミスがありました。

5.  company\_industry（業種）
    

「4. 欠損がない場合どのようなデータが入っているのか」実行結果134, 135行目より、company\_industryには複数のラベルが格納されたレコードが存在することが確認できました。

私は最初多クラス分類のマルチクラス分類にしようと考えていました。しかし、複数の業種が格納されたレコードが多ければ、マルチラベル分類として考えたほうが良さそうです。そこで、業種が複数あるレコード数と割合を調査しました。

```Python
# 業種が複数あるレコード数を調べる
targetCharacter = ','
multipleIndustryRows = 0
for i in list(df_dropna["company_industry"]):
    i = str(i)
    if targetCharacter in i:
        multipleIndustryRows += 1
print(multipleIndustryRows)
print(df_dropna.shape[0])
print(multipleIndustryRows / df_dropna.shape[0])
# （業種が複数個であるレコード数） / （業種の欠損値を省いたレコード数）
```

```Python
###実行結果###
586587
1083639
0.5413121897606121
```

結果から、半分以上レコードが複数の業種ラベルを格納しています。