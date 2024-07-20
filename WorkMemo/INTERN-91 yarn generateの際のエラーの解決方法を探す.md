*   1 [0. 結論](#0.結論)
*   2 [1. 概要](#1.概要)
*   3 [2. エラー](#2.エラー)
*   4 [3. 解決方法](#3.解決方法)

# 0. 結論
[nuxt generateでpathの不一致エラーが出たときの対処【SAKUSAKU -Web制作のTipsおつまみブログ-】 | 株式会社SAKURUG 
Windowsのバックスラッシュの問題だったらしい](https://sakurug.co.jp/news/6161/)

# 1. 概要
[INTERN-91: yarn generateの際のエラーの解決方法を探す完了](https://pantarhei-hub.atlassian.net/browse/INTERN-91)
 

yarn generateをして、Vue.jsやNuxt.jsの拡張子である.vueファイルをブラウザが解釈できる状態になるようにしなければならない。

# 2. エラー
leadknock-frontendをyarn generateするとNuxt Fatal errorになる。 

```
Nuxt Fatal Error
Error: Path C:/hoge/leadknock-frontend/app-prd.yaml is not in cwd C:\hoge\leadknock-frontend
error Command failed with exit code 1.
info Visit https://yarnpkg.com/en/docs/cli/run for documentation about this command.
```
`ようするにNuxt.jsプロジェクトの作業ディレクトリ内にファイルが存在してないよってこと。
よくみたら、
cwdの後の文字がスラッシュがバックスラッシュになっている。C:\hoge\leadknock-frontend
C:/hoge/leadknock-frontend/app-prd.yaml →C:\hoge\leadknock-frontend
多分これが問題だなー`

3. 解決方法

`参考サイト `

上記を見たところ、どうやらWindowsのバックスラッシュの問題だったらしい。

下記を修正するといいらしい
leadknock-frontend\node_modules\globby\gitignore.js

```
// gitignore.js#48
const ensureAbsolutePathForCwd = (cwd, p) => {
+	p = path.normalize(p);
	cwd = slash(cwd);
	if (path.isAbsolute(p)) {
		if (p.startsWith(cwd)) {
			return p;
		}

		throw new Error(`Path ${p} is not in cwd ${cwd}`);
	}

	return path.join(cwd, p);
};
```
書き換えたらgenerateできた。

ふざけんな！！！ 

前のコードも置いておく
```
const ensureAbsolutePathForCwd = (cwd, p) => {
	cwd = slash(cwd);
	if (path.isAbsolute(p)) {
		if (slash(p).startsWith(cwd)) {
			return p;
		}

		throw new Error(`Path ${p} is not in cwd ${cwd}`);
	}

	return path.join(cwd, p);
};
```
