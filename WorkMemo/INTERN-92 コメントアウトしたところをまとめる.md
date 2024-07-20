*   1 [0. 結論](#0.結論)
*   2 [1. 概要](#1.概要)
*   3 [2. コメントアウト箇所](#2.コメントアウト箇所)
    *   3-1 [2-1. ログイン認証](#2-1.ログイン認証)
    *   3-2 [2-2. レイアウト](#2-2.レイアウト)
    *   3-3 [2-3. 設定](#2-3.設定)
    *   3-4 [2-4. 営業リストインポート](#2-4.営業リストインポート)
    *   3-5 [2-5. 営業リスト](#2-5.営業リスト)

# 0. 結論

`$api`、`$auth`関連をコメントアウトすれば大抵動く

# 1. 概要

[https://pantarhei-hub.atlassian.net/browse/INTERN-92]

# 2. コメントアウト箇所

## ログイン認証

`nuxt.config.jsnuxt.config.js`

```
#80行目
router: {
  middleware: ['auth'],
},
```
## レイアウト
`leadknock-frontend\layouts\default.vue`
```
#20行目
<img v-if="$auth.user.avatar" class="inline-block h-12 w-12 rounded-full ring-2 ring-white" :src="$auth.user.avatar"/>
<avatar
  v-else
  :username="$auth.user.last_name"
  background-color="#E6F6F8"
  color="#6783B3"
></avatar>

#29行目
<p>{{ $auth.user.last_name }}{{ $auth.user.first_name }}</p>
```
## 設定

`leadknock-frontend\components\settings\SettingsContent.vue`
```
#12行目
<b>{{$auth.user.last_name + $auth.user.first_name}}</b>

#18行目
<b>{{$auth.user.email}}</b>
```
## 営業リストインポート

`leadknock-frontend\pages\import_data\list\index.vue`
```
#342行目
const res = await this.$api.salelist.getListJob((res) => {
  return res.data;
});
this.jobList = res.data.list_job

#348行目
this.dataTable = res.data.list_job
```
leadknock-frontend\pages\import_data\create\index.vue
```
#133行目
const res = await this.$api.project.getJobProjects((res) => {
  return res.data;
});
this.listProject = res.data.projects
```
## 営業リスト

`leadknock-frontend\pages\salelist\list\index.vue`
```
#318行目
const res = await this.$api.salelist.getSaleList((res) => {
  return res.data;
});
this.dataTable = res.data.data;
this.salesList = res.data.data;
this.userName =
  this.$auth.user.last_name + " " + this.$auth.user.first_name;
```


