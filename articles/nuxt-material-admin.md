---
title: "Nuxt.jsで管理画面を作って、GitHub Pagesでデプロイする：Vue.js Step by Step"
emoji: "🤖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["nuxtjs","管理画面","github-pages"]
published: true
---

このシリーズでは、Vue.jsを簡単なところから使い始めて、徐々に本格的に使う手順を記録しています。


## プロジェクトのセットアップ

Vue-CLIで、簡単に

```
$ vue init moeddami/nuxt-material-admin my-project
$ cd my-project
$ yarn install
```

## 動作確認

localhost:3000 で動作確認できます。

```
$ yarn dev
```

### Github Pagesでデプロイする

Nuxt.jsで作ったアプリをGithub Pagesでデプロイする場合、masterブランチのdocsディレクトリを公開するのが簡単だと思います。

そこで、ビルド先をdocsにするよう、nuxt.config.jsに generate: を追加します。

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

    /*
    ** You can extend webpack config here
    */
    extend(config, ctx) {

    }
  },

  generate: {
    dir: 'docs'
  }
```

それから、公開するファイルをビルドします。

```
$ yarn build
```

これで、docs ディレクトリに静的ファイルが生成されました。

GitHubに、docsディレクトリごとコミットします。


## 公開したアプリ

今回、作成した管理画面を GitHub Pages で公開しています。

- デモページ(GitHub Pages)  
  https://ycatch.github.io/vue-app/  
- ソースコード(GitHub)  
  https://github.com/ycatch/vue-nuxt-app

![./images/install_nuxtjs/demo-nuxt-project.png](https://storage.googleapis.com/zenn-user-upload/cvsdxuqjzg8nvr517vfcak76pbkk)


## 参考になるページ

- moeddami / nuxt-material-admin 
  https://github.com/moeddami/nuxt-material-admin/

- Vue-CLI Boilerplate based on Nuxt and vue-material-admin template
https://vuejsexamples.com/vue-cli-boilerplate-based-on-nuxt-and-vue-material-admin-template/

