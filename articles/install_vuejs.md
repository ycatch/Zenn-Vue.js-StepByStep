---
title: "Vue.jsでアプリを作って、GitHub Pagesでデプロイする：Vue.js Step by Step"
emoji: "🤖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Vuejs", "Vue CLI"]
published: false
---

[Vue.js](https://v3.ja.vuejs.org/)は、フロントエンド開発フレームワークです。2020年9月に、Vue 3.0が公開されました。

「Progressive Framework」という特徴があり、jQueryとか使っていた人が、段階的に導入していくことができます。

なので、最新のフロントエンド開発に初めて取り組む人に、いい感じだと思います。というか、私がそうです。

この記事では、Vue.jsを簡単なところから使い始めて、徐々に本格的に使う手順を記録していきます。まずは、Vue.jsの導入。Vue.jsを使い始めて、簡単なWebアプリをつくって、GitHub Pagesにデプロイするところまでやります。

## 公式ページ

- Vue.js
  https://v3.ja.vuejs.org/


## チュートリアル

Vue.jsは、既存のWebサイトに組み込んで使うことができます。これが、一番試しやすいでしょう。公式チュートリアルをやると、基本的なコードの書き方を体験できると思います。ブラウザのなかで実行できるので、お手軽です。

- 基本的な使い方 > はじめに | Vue.js 3.0
  https://v3.ja.vuejs.org/guide/introduction.html


## Vue-CLIで、アプリケーションを作成する

次は、Vue.jsを使って、Webアプリケーションを作ります。

### vue-cliをインストールする

これには、Vue-CLIを使います。

- Vue CLI
  https://cli.vuejs.org/

インストールします。

```
$ npm install -g @vue/cli
$ vue --version
```

### vue-cliで、アプリケーションを作成する

アプリケーションを作成します。

```
$ vue create vue-app
```

たったこれだけ。

どの環境で作るか、メニュー形式で選択できるので、順番に答えていきます。最初は、デフォルトの選択肢を選べばいいんじゃないかな。

### 動作確認

できたアプリケーションをローカル環境で起動してみます。

```
$ cd vue-app
$ yarn serve
|
| App running at:
| - Local:   http://localhost:8080/
| - Network: http://192.168.1.4:8080/
|
| Note that the development build is not optimized.
| To create a production build, run yarn build.
```

ブラウザで http://localhost:8080/ にアクセスすると、こんなふうに表示されます。

![./images/install_vuejs/first_app.png](https://storage.googleapis.com/zenn-user-upload/jc3y8yut1uh9twgizscvpyixsdf8)

vue-app ディレクトリは、GitHub にリポジトリを作って格納しておきましょう。

## GitHub Pagesでデプロイする

では、Webアプリを静的サイトとして生成して、GitHub Pagesで公開してみましょう。GitHub Pagesには、個人のユーザーアカウントにひもづくページと、リポジトリにひもづくページがあります。今回は、リポジトリに対して作成します。

### ビルドする

GitHub Pagesは、docsディレクトリか、gh-pagesブランチのファイルを出力します。今回は、docsディレクトリの内容を表示します。そこで、リポジトリのホームディレクトリに、vue.config.js というファイルを作成して、次のように書き込みます。

vue.config.js 
```js
module.exports = {
  outputDir: 'docs',
  assetsDir: './',
  publicPath: './',
}
```

つぎに、表示するファイルをビルドします。

```
$ yarn build
| DONE  Compiled successfully in 22541ms                                                                         20:06:29
| 
|  File                                 Size                                   Gzipped
|
|  docs\js\chunk-vendors.ff672a17.js    89.66 KiB                              32.14 KiB
| docs\js\app.225fd15b.js              4.58 KiB                               1.63 KiB
| docs\css\app.fb0c6e1c.css            0.33 KiB                               0.23 KiB
|
| Images and other types of assets omitted.
| 
| DONE  Build complete. The docs directory is ready to be deployed.
| INFO  Check out deployment instructions at https://cli.vuejs.org/guide/deployment.html
| 
| Done in 31.22s.
```

これで、docs ディレクトリに静的ファイルが生成されました。

GitHubに、docsディレクトリごとコミットします。

### GitHub Pagesを設定する

1. GitHubで、対象のリポジトリにアクセスする
2. 上部の「Settings」をクリック
3. Pagesタブを選択
4. Source として、Masterブランチのdocs ディレクトリを選択する
5. Save ボタンをクリック

![./images/install_vuejs/github_pages_settings.png](https://storage.googleapis.com/zenn-user-upload/naobyx3fvqsjscorgmcxncgxyp6v)


## 公開したアプリ

これで、vue.jsで作成したアプリケーションを、GitHub Pagesで公開できました。

- GitHub：ycatch/vue-app
  https://github.com/ycatch/vue-app

- GitHub Pages
  https://ycatch.github.io/vue-app/


## 参考になるページ

- Vue.js の"The Progressive Framework"という設計思想がすごく刺さった
  https://snowlong.hatenablog.com/entry/2017/03/27/190715

- 第1回　プログレッシブフレームワーク Vue.js：Vue.js入門 ―最速で作るシンプルなWebアプリケーション｜gihyo.jp … 技術評論社
  https://gihyo.jp/dev/serial/01/vuejs/0001
