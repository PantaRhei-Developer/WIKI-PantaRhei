*   1 [0\. 結論](#0.-結論)
*   2 [1\. 概要](#1.-概要)
*   3 [2\. 第1章](#2.-第1章)
    *   3.1 [VueとNuxtの関係](#VueとNuxtの関係)
        *   3.1.1 [Vueとは](#Vueとは)
        *   3.1.2 [Vue3の特徴](#Vue3の特徴)
        *   3.1.3 [Nuxtとは](#Nuxtとは)
        *   3.1.4 [Nuxt3とは](#Nuxt3とは)
        *   3.1.5 [SSR・CSR・ユニバーサル・SSG・ISG・ハイブリッドレンダリング](#SSR・CSR・ユニバーサル・SSG・ISG・ハイブリッドレンダリング)
        *   3.1.6 [Nuxt3のハイブリッドレンダリングとNitro](#Nuxt3のハイブリッドレンダリングとNitro)
    *   3.2 [Nuxtの環境構築](#Nuxtの環境構築)
    *   3.3 [Nuxtプロジェクトの作成と実行](#Nuxtプロジェクトの作成と実行)
*   4 [3\. 第2章](#3.-第2章)
    *   4.1 [第2章気になったこと](#第2章気になったこと)
*   5 [3\. 第3章](#3.-第3章)
    *   5.1 [Nuxtルーティングの基本](#Nuxtルーティングの基本)
        *   5.1.1 [ルーティング表示領域を設定するNuxtPageタグ](#ルーティング表示領域を設定するNuxtPageタグ)
        *   5.1.2 [Nuxtはファイルシステムルータ](#Nuxtはファイルシステムルータ)
        *   5.1.3 [リンク生成はNuxtLinkタグ](#リンク生成はNuxtLinkタグ)
        *   5.1.4 [ルートパラメータは\[\]のファイル名](#ルートパラメータは[]のファイル名)
        *   5.1.5 [useRoute()](#useRoute())
        *   5.1.6 [ルートパラメータ付きのリンク作成](#ルートパラメータ付きのリンク作成)
        *   5.1.7 [ルーティングを制御するルータオブジェクト](#ルーティングを制御するルータオブジェクト)
    *   5.2 [レイアウト機能](#レイアウト機能)
        *   5.2.1 [レイアウトの適応](#レイアウトの適応)
    *   5.3 [ヘッダ情報の変更機能](#ヘッダ情報の変更機能)
        *   5.3.1 [ヘッダ情報を変更するuseHead()](#ヘッダ情報を変更するuseHead())
    *   5.4 [まとめ](#まとめ)
    *   5.5 [単語](#単語)

# 0\. 結論

# 1\. 概要

[https://pantarhei-hub.atlassian.net/browse/INTERN-23](https://pantarhei-hub.atlassian.net/browse/INTERN-23)Can't find link

# 2\. 第1章

## VueとNuxtの関係

### Vueとは

JSコード上の変数と**DOM要素**が自動的に連動する**リアクティブシステム**をコアに含みながらも、軽量で、軽快に動作するフレームワーク。

Vueプロジェクトに含まれる主なモジュールとして

*   **Vue Router**･･･シングルページアプリケーションを手軽に実現できる
    
*   **Pinia**･･･コンポーネント間横断でデータを管理できるステート管理モジュール
    
*   **Vitest･Vue Test Utils**･･･Vueのユニットテストを容易にできる。
    

などがあり、これらをひとまとめにして実行ファイルにするビルルドツールとして**Vite**が用いられている。

### Vue3の特徴

*   **TypeScript**の採用･･･型安全なアプリケーションが作成可能に
    
*   **Composition API**の採用･･･コード記述量の低減
    
*   **Vite**(**ヴィート**)の標準採用･･･Webpackよりもビルドが早い
    

### Nuxtとは

Vueに関連するモジュール類をワンパックにし、設定を別途記述する必要がないような状態で利用できるようにするもの。 さらに、非同期でデータを簡単に取得できる機能や**サーバサイドレンダリング機能**なども追加されている。

### Nuxt3とは

Vue3と同等にTypeScriptによる型安全なアプリケーションが作成可能。  
Nuxtの主な機能


| 機能 | 内容 | 章 |
| --- | --- | --- |
| ファイルシステムルーティング | フォルダ構成がそのままルーティングインケ設定情報とできる | 第3章 |
| レイアウト | 画面の共通レイアウトが設定できる | 第3章 |
| ステート管理 | Piniaを利用しなくてもステート管理できる | 第2章 |
| オートインポート | インポートを記述しなくてもモジュールを利用できる | 第2章 |
| データ取得関数 | JavaScript標準のfetch()関数をより使いやすくした関数が利用できる | 第4章 |
| エラー処理 | 種々のエラー処理を挟み込むことができる | 第6章 |
| ミドルウェア | 画面遷移の前に処理を挟み込むことができる | 第7章 |
| サーバAPIエンドポイント | Web APIなどのエンドポイントをNuxt単独で用意できる | 第5章 |
| レンダリングモードの切替 | 4種のレンダリングモードをパスごとに設定できる | 第8章 |


### SSR・CSR・ユニバーサル・SSG・ISG・ハイブリッドレンダリング

| 機能 | 内容 | 短所 |
| --- | --- | --- |
| SSR Server-Side Rendering | 各ページの表示速度が速い SEOに強い | 即応性に欠ける |
| CSR Client-Side Rendering | 即応性が高い | 初回表示速度が遅い SEOに弱い |
| ユニバーサル | 各ページの表示速度が速い 即応性が高い SEOに強い | Nuxtのような専用フレームワークが必要 |
| SSG Static Site Generation | 各ページの表示速度が非常に速い | データの変更に合わせてページ内容が変更できない |
| ISG Incremental Static Generation | 各ページの表示速度が非常に速い データの変更に合わせてページ内容が変更できる | ページ内容変更が一定間隔になるため、その都度のデータ変更ができない |



Nuxt3では、上記のいずれかを選択するというのではなく、ひとつのアプリケーション内で混在させることができる**ハイブリッドレンダリング**(**Hybrid Rebdering**)に対応している。どのレンダリング方式を選択するかはパスごとに選択できる。

### Nuxt3のハイブリッドレンダリングとNitro

サーバレスコンピューティング上で動作させる際に不具合が起きていたが、Nuxt3の基幹部分(サーバエンジン)に据えられたことでデプロイ先が増えた。

## Nuxtの環境構築

*   Visual Studio Cord
    
*   Visual Studio Cordの拡張機能 Volar
    
*   Visual Studio Cordの拡張機能 TypeScript Vue Plugin
    
*   Node.js
    

上記の最新版をそれぞれインストール。

## Nuxtプロジェクトの作成と実行

```
// Nuxtプロジェクト作成コマンド
npx nuxi init プロジェクト名

//npmパッケージのインストールコマンド
npm install

//開発用サーバ起動コマンド
npm run dev
```

# 3\. 第2章

## 第2章気になったこと

hoge: _stringはtsの型をつけている_

**イベントオブジェクト**

\*\*`Event`\*\*オブジェクトのプロパティを参照することで、さまざまな情報を取得することができる

Event.targetの場合イベントが発生した要素を取得 [![](https://tcd-theme.com/wp-content/uploads/2022/07/cropped-favicon-new-32x32.png)【JavaScriptの基本】イベントオブジェクト – ワードプレステーマTCD](https://tcd-theme.com/2022/09/javascript-eventobject.html)

_scoped_

# 3\. 第3章

## Nuxtルーティングの基本

Vueアプリケーションで画面推移(ルーティング)を行う場合、**Vue Router**を利用する。  
  
Vue Routerでは、ルーティング設定情報をファイルに記述する必要がある。  
→Nuxtでは不要

```
/member/memberDetail/1234
```

**ルートパラメータ**･･･リンクパスの末尾の「1234」はクリックするオブジェクトによって変化する。

### **ルーティング表示領域を設定するNuxtPageタグ**

NuxtPageタグはルートタグとしては使えない。

```
//これだとできない
<template>
  <NuxtPage/>
<template>`

//divタグ、別のタグで囲む必要がある
<template>
  <div>
    <NuxtPage/>
  </div>
<template>
```

### **Nuxtはファイルシステムルータ**

Nuxtでは、画面表示用コンポーネントはすべてpagesフォルダに格納することになっている。  
また、単に格納しているだけではなく、格納するファイルパス構造がそのままルーティングパスになる。  
→**ファイルシステムルータ**と呼ぶ  
ルートに該当するファイルは、index.vue

### **リンク生成はNuxtLinkタグ**

```
<NuxtLink v-bind:to="{name: 'ハイフン区切りの画像用コンポーネントファイルパス'}">
//member/memberList.vueの場合
<NuxtLink v-bind:to="{name: 'member-memberList'}">
```

### **ルートパラメータは\[\]のファイル名**

id.vueとすると、このidはルートパラメータとして認識されない。  
代わりに\[id\].vueとする。

### useRoute()

現在のルートに関する情報が格納された**ルートオブジェクト**を取得できる

| プロパティ | 内容 | 例 |
| --- | --- | --- |
| name | ルーティング名 | member-memberDetail-id |
| fullPath | pathとhashとqueryのすべてが含まれたパスの文字列 | member-memberDetail/47783#session?name=tanaka |
| path | ルーティングパス文字列 | member-memberDetail/47783 |
| hash | ハッシュ(#以降の文字列) | #session |
| query | クエリ情報(?以降の情報){name: tanaka} | {name:tanaka} |
| params | ルートパラメータ | {id:47783} |


### **ルートパラメータ付きのリンク作成**

```
<NuxtLink v-bind:to="{name: 'member-memberDetail-id', params: {id: id}}">
```

### **ルーティングを制御するルータオブジェクト**

| メソッド | 内容 |
| --- | --- |
| push() | 指定パスに推移する |
| replace() | 現在のパスを置き換える |
| back() | 履歴上のひとつ前の画面に戻る |
| forward() | 履歴上のひとつ次の画面に進む |
| go() | 履歴上の指定の画面に進む |


## レイアウト機能

各画面の共通部分を集約する。  
`layouts/default.vue`にすることが決まっている。  
その際は`NuxtPage`を記述していたところに`slot`タグを使う。

### **レイアウトの適応**

NuxtLayoutを使う。

```
<NuxtLayout>
  <NuxtPage/>
</NuxtLayout>
```

レイアウトを無効にしたい場合は

```
definePageMeta({ layout: false });
```

## ヘッダ情報の変更機能

### ヘッダ情報を変更するuseHead()

ページのタイトルが帰られるようになる。

| プロパティ名 | データ型 | 内容 |
| ------------ | -------- | ---- |
| title        | string   | タイトルタグの設定 |
| titleTemplate | string/アロー関数 | タイトルタグを自動的に設定 |
| meta         | 配列     | metaタグの設定 |
| link         | 配列     | linkタグの設定 |
| style        | 配列     | styleタグの設定 |
| script       | 配列     | scriptタグの設定 |
| noscript     | 配列     | noscriptタグの設定 |
| htmlAttrs    | オブジェクト | htmlタグの属性の設定 |
| bodyAttrs    | オブジェクト | bodyタグの属性の設定 |

## まとめ

## 単語

**ステート管理**

**ユニットテスト**(**単体テスト**)

プログラムを構成する比較的小さな単位(ユニット)が個々の機能を正しく果たしているかどうかを検証するテスト。

[![](https://www.techmatrix.co.jp/common/img/common/favicon.ico)単体テスト(ユニットテスト)とは](https://www.techmatrix.co.jp/t/quality/unittest.html)

**レンダリング 画面表示に必要なHTMLデータの生成 クローラー**

CSR、SSR、SSG [![](https://static.zenn.studio/images/logo-transparent.png)CSR、SSR、SSGの違い](https://zenn.dev/takuyakikuchi/articles/2f7e54bdafce52)

コンポーネント