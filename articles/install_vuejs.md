---
title: "Vue.jsでアプリを作って、GitHub Pagesでデプロイする：Vue.js Step by Step"
emoji: "🌟"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["Vuejs"]
published: false
---

[Vue.js](https://v3.ja.vuejs.org/)は、フロントエンド開発フレームワークです。2020年9月に、Vue 3.0が公開されました。

「Progressive Framework」という特徴があり、jQueryとか使っていた人が、段階的に導入していくことができます。

なので、最新のフロントエンド開発に初めて取り組む人に、いい感じだと思います。というか、私がそうです。

この記事では、Vue.jsを簡単なところから使い始めて、徐々に本格的に使う手順を記録していきます。まずは、Vue.jsの導入。Vue.jsを使い始めて、簡単なWebアプリをGitHub Pagesにデプロイするところまでやります。

## 公式ページ

- Vue.js
  https://v3.ja.vuejs.org/


## チュートリアル

まずは、既存のWebサイトに組み込んで使ってみましょう。

公式チュートリアルが充実しているので、これをやると、基本的なコードの書き方を体験できると思います。ブラウザのなかで実行できるので、お手軽です。

- 基本的な使い方 > はじめに | Vue.js 3.0
  https://v3.ja.vuejs.org/guide/introduction.html


## Vue-CLIで、アプリケーションを作成する

次は、Vue.jsを使って、Webアプリケーションを作ります。これには、Vue-CLIを使います。

- Vue CLI
  https://cli.vuejs.org/

インストールします。

```
$ npm install -g @vue/cli
$ vue --version
```

アプリケーションを作成します。

```
$ vue create vue-app
```

たったこれだけ。どの環境で作るか、メニュー形式で選択できるので、順番に答えていきます。最初は、デフォルトの選択肢を選べばいいんじゃないかな。

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

ブラウザで、こんなふうに表示されます。

![./images/install_vuejs/first_app.png](https://storage.googleapis.com/zenn-user-upload/jc3y8yut1uh9twgizscvpyixsdf8)



## 参考になるページ


- Vue.js の"The Progressive Framework"という設計思想がすごく刺さった
  https://snowlong.hatenablog.com/entry/2017/03/27/190715

- 第1回　プログレッシブフレームワーク Vue.js：Vue.js入門 ―最速で作るシンプルなWebアプリケーション｜gihyo.jp … 技術評論社
  https://gihyo.jp/dev/serial/01/vuejs/0001