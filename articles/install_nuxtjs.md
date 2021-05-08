---
title: "Nuxt.jsでアプリを作って、GitHub Pagesでデプロイする：Vue.js Step by Step"
emoji: "🤖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["vuejs","nuxtjs","github-pages"]
published: true
---

このシリーズでは、Vue.jsを簡単なところから使い始めて、徐々に本格的に使う手順を記録しています。今回は、Vue.js製のアプリケーションフレームワークNuxt.jsを使い始める手順です。ほとんどは[公式サイトのチュートリアル](https://ja.nuxtjs.org/docs/2.x/get-started/installation)に書いてありますが、Github Pagesにデプロイするには、ちょっと工夫が必要です。

## Nuxt.jsの特徴

Nuxt.jsは、Vue.jsでWebアプリケーションを作るときの土台になるツールです。Webアプリに必要なライブラリがいろいろ入ってますし、ページを追加すると、自動的にルーティングしてくれます。何より、サーバーサイドレンダリングや静的サイトジェネレーションに対応しています。

2021年5月現在、Vue.js Ver2.0に対応しています。


- Nuxt.js - The Intuitive Vue Framework  
  https://nuxtjs.org/
- Nuxt.js - ユニバーサル Vue.js アプリケーション  
  https://ja.nuxtjs.org/


## まとめて生成する

これは、次のcreateコマンドで簡単にできます。途中、利用するライブラリや開発ツールを確認してくるので、順番に答えていきます。

```
$ yarn create nuxt-app my-nuxt-project
|
| ✨  Generating Nuxt.js project in nuxt-app
| ? Project name: nuxt-app
| ? Programming language: JavaScript
| ? Package manager: Yarn
| ? UI framework: Vuetify.js
| ? Nuxt.js modules: Axios - Promise based HTTP client
| ? Linting tools: ESLint, Prettier
| ? Testing framework: None
| ? Rendering mode: Single Page App
| ? Deployment target: Server (Node.js hosting)
| ? Development tools: jsconfig.json (Recommended for VS Code if you're not using typescript)
| ? Continuous integration: None
| ? Version control system: Git
```

できたら、次のコマンドで動作確認します。

```
$ cd my-nuxt-project
$ yarn dev
```

http://localhost:3000/ に、こんなアプリができています。ここでは、pagesディレクトリに「inndex.vue」と「inspire.vue」というファイルがあって、そこから自動的にルーティングを設定しています。

![./images/install_nuxtjs/my-nuxt-project.png](https://storage.googleapis.com/zenn-user-upload/3xjfj9tkr89n3yidgajuiu4t9u48)


## Github Pagesでデプロイする

Nuxt.jsで作ったアプリをGithub Pagesでデプロイする場合、masterブランチのdocsディレクトリを公開するのが簡単だと思います。

そこで、ビルド先をdocsにするよう、nuxt.config.jsに次のコードを追加します。base: には、Githubのリポジトリ名を指定します。両端のスラッシュを忘れずに。

```js:nuxt.config.js
  router: {
    base: '/my-nuxt-project/'
  },

  generate: {
    dir: 'docs'
  },
}
```

それから、公開するファイルをビルドします。

```
$ yarn build
```

これで、docs ディレクトリに静的ファイルが生成されました。

GitHubに、docsディレクトリごとコミットします。

## 公開したアプリ

今回、nux.jsで作成したアプリケーションを GitHub Pages で公開しています。このデモページでは、ダークモードをオフにして、Helloというページを追加しています。

- デモページ(GitHub Pages)  
  https://ycatch.github.io/vue-app/  
- ソースコード(GitHub)  
  https://github.com/ycatch/vue-nuxt-app

![./images/install_nuxtjs/demo-nuxt-project.png](https://storage.googleapis.com/zenn-user-upload/cvsdxuqjzg8nvr517vfcak76pbkk)


## 参考になるページ

- Nuxt.js - The Intuitive Vue Framework
  https://nuxtjs.org/

- Nuxt.js - ユニバーサル Vue.js アプリケーション
  https://ja.nuxtjs.org/


### チュートリアル

- 【完全ガイド】ゼロからしっかり理解したい人向けのNuxt.js入門 | アールエフェクト
  https://reffect.co.jp/vue/nuxt-js-first-step

- GitHub PagesとNuxt.jsでポートフォリオ公開 - Qiita
  https://qiita.com/Anderiens/items/a4c5783b5197de682329

