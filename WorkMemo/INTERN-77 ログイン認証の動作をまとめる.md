*   1 [0. 結論](#0.結論)
*   2 [1. 概要](#1.概要)
*   3 [2. メモ](#2.メモ)

# 0. 結論

  ```
router: {
  middleware: ['auth'],
},
   ```

`layouts/default.vue`
   ```
<div class="column is-narrow pr-0">
  <img v-if="$auth.user.avatar" class="inline-block h-12 w-12 rounded-full ring-2 ring-white" :src="$auth.user.avatar"/>
  <avatar
    v-else
    :username="$auth.user.last_name"
    background-color="#E6F6F8"
    color="#6783B3"
  ></avatar>
</div>
   ```
上記をコメントアウトする

# 1. 概要

https://pantarhei-hub.atlassian.net/browse/INTERN-77 

# 2. メモ

nuxt.config.js

   ```
//コメントアウト
//ここから
router: {
  middleware: ['auth'],
},
//ここまで

auth: {
    redirect: {
      login: '/login',
      logout: '/',
      callback: '/login',
      home: '/',
    },
    strategies: {
      local: {
        url: process.env.API_URL,
        endpoints: {
          login: { url: '/api/login', method: 'post' },
          refresh: { url: '/api/token/refresh', method: 'post' },
          user: { url: '/api/me', method: 'get' },
          logout: { url: '/api/logout', method: 'post' },
        },
        token: {
          property: 'access',
          maxAge: 60 * 60,
        },
        refreshToken: {
          maxAge: 60 * 60 * 24 * 30,
        },
        user: {
          property: 'user',
        }
      },
    },
  }
   ```
でログイン認証している

`router`をコメントアウトすることで、ログイン認証されていなくても閲覧できるようになる。

Cannot read properties of null (reading 'avatar')と表示されてしまいアクセスできない。
どこにavatarがあるか探したところ、`layouts/default.vue`に書かれていた。

どうやら`layouts/default.vue`に書かれている内容は、`layouts`が指定いされていないすべてのページに適応されるらしい。

  ```
<div class="column is-narrow pr-0">
  <img v-if="$auth.user.avatar" class="inline-block h-12 w-12 rounded-full ring-2 ring-white" :src="$auth.user.avatar"/>
  <avatar
    v-else
    :username="$auth.user.last_name"
    background-color="#E6F6F8"
    color="#6783B3"
  ></avatar>
</div>
  ```
なのでコメントアウトしてみた結果、UIが表示された。
