---
title: "Nuxt.jsで管理画面を作って、GitHub Pagesでデプロイする：Vue.js Step by Step"
emoji: "🤖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["nuxtjs","管理画面","github-pages"]
published: true
---

このシリーズでは、Vue.jsを簡単なところから使い始めて、徐々に本格的に使う手順を記録しています。今回は、Nuxt.jsとmaterial designを使った管理画面を作ります。そのために、nuxt-material-admin を使います。

- moeddami / nuxt-material-admin 
  https://github.com/moeddami/nuxt-material-admin/

![./images/nuxt-material-admin/demo_admin.png](https://storage.googleapis.com/zenn-user-upload/ryxqcxemyr45ec2ra0kumln2s37l)

こんな感じで、複数ページの管理画面ができあがります。


## nuxt-material-adminのセットアップ

nuxt-material-adminは、Vue-CLIで、簡単にセットアップできます。

```bash
$ vue init moeddami/nuxt-material-admin my-project
$ cd my-project
$ yarn install
```

## 動作確認

localhost:3000 で動作確認できます。

```bash
$ yarn dev
```

## Github Pagesでデプロイする

Github Pagesでデプロイするため、nuxt.config.js の設定を変更します。

### mode: を ssr: に変更する

nuxt.jsでは、modeオプションが非奨励なので、ssrオプションに変更します。

```js:nuxt.config.js
module.exports = {
//mode: 'spa',
  ssr: false,
```

### babel: を設定する

Nuxt.jsで、BabelのWarningが大量に出るので、build:オプションに babel: オプションを設定します。

```js:nuxt.config.js
  /*
  ** Build configuration
  */
  build: {
    transpile: ['vuetify/lib'],
    plugins: [new VuetifyLoaderPlugin()],
    loaders: {
      stylus: {
        import: ["~assets/style/variables.styl"]
      }
    },

    babel: {
        plugins: [['@babel/plugin-proposal-private-methods', { loose: true }]],
    },

    /*
    ** You can extend webpack config here
    */
    extend(config, ctx) {

    }
  },
```

### router: を設定する

Githubのリポジトリ名を router: の base: オプションに設定します。前後のスラッシュを忘れずに。

```js:nuxt.config.js
  router: {
    base: '/<repository-name>/'
  },
```

### ビルド先を指定する

Nuxt.jsで作ったアプリをGithub Pagesでデプロイする場合、masterブランチのdocsディレクトリを公開するのが簡単だと思います。

そこで、ビルド先をdocsにするよう、nuxt.config.jsに generate: を追加します。

```js:nuxt.config.js
  generate: {
    dir: 'docs'
  }
```

実際の nuxt.config.js は、以下を参照してください。

- [nuxt.config.js](https://github.com/ycatch/nuxt-material-admin/blob/main/nuxt.config.js)


### ビルドする

それから、公開するファイルをビルドします。

```bash
$ yarn build
```

これで、docs ディレクトリに静的ファイルが生成されました。

あとは、GitHubに docsディレクトリごとコミットします。そして、Github pagesで公開します。


## 公開したアプリ

今回、作成した管理画面を GitHub Pages で公開しています。

- デモページ(GitHub Pages)  
  https://ycatch.github.io/nuxt-material-admin/  
- ソースコード(GitHub)  
  https://github.com/ycatch/nuxt-material-admin

