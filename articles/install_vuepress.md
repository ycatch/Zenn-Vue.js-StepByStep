---
title: "VuePressを、GitHub Pagesでデプロイする：Vue.js Step by Step"
emoji: "🤖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["vuejs","vuepress","github-pages"]
published: false
---

このシリーズでは、Vue.jsを簡単なところから使い始めて、徐々に本格的に使う手順を記録しています。Nuxt.jsを使うなら、いっそ静的サイトジェネレータのVuePressでいいんじゃないか。

## VuePressとは

VuePressは、vue.jsによる静的サイトジェネレータです。特定のディレクトリにmarkdownファイルを放り込むと、自動的にページを作成してくれます。Nuxt.jsがアプリケーションの開発フレームワークとして設計されているのに対して、VurePressは、一種のCMSになっています。

- VuePress
  https://vuepress.vuejs.org/

## VurPressサイトを作る

### インストールする

```
$ yarn init
$ yarn add - D vuepress
```


### ページを追加する

ここでは、コンテンツをsrc/ ディレクトリに追加します。

```
$ mkdir src
```

公式ドキュメントでは docs/ を推奨していますが、GitHub Pages の公開ディレクトリと競合するため、docs/ 以外の名前でディレクトリ作成します。

そして、このsrc/に、README.mdを追加します。


### vuepress 用のコマンドを追記する

package.json に vuepress 用のコマンドを追記します。コンテンツディレクトリのsrc/にあわせて、devコマンドとbuildコマンドを設定します。

```json
{
  "name": "vue-press",
  "version": "1.0.0",
  "main": "index.js",
  "repository": "https://github.com/XXXXXXX/vue-press.git",
  "author": "XXXXXXX",
  "license": "MIT",
  "scripts": {
    "src:dev":"vuepress dev src",
    "src:build":"vuepress build src"
  },
  "devDependencies": {
    "vuepress": "^1.8.2"
  }
}
```

### 動作確認

次のコマンドで、ローカルで動作確認します。

```
$ yarn src:dev
```

http://localhost:8080/ で表示できます。


### ナビゲーションとサイドバーを設定する

src/.vuepress/config.js で設定できます。


## Github Pages でデプロイする


### ビルド設定

src/.vuepress/config.jsに、以下を追加します。このとき、ビルド先のdestを、docs/ にしています。


```js:src/.vuepress/config.js
module.exports = {
  /**
   * Ref：https://v1.vuepress.vuejs.org/config/#title
   */
  title: 'Hello VuePress',
  /**
   * Ref：https://v1.vuepress.vuejs.org/config/#description
   */
  description: description,
  dest: 'docs/',
  base: '/vue-press/',
```

### ビルドする

静的ページを生成します。

```
$ yarn src:build
```


### Github pagesで公開する

今回は、masterブランチのdocsディレクトリを公開することを想定しています。

あとは、GitHubに、docsディレクトリごとコミットします。


## 公開したアプリ

今回、VuePressで作成したサイトを GitHub Pages で公開しています。

- デモページ(GitHub Pages)  
  https://ycatch.github.io/vue-press/
- ソースコード(GitHub)  
  https://github.com/ycatch/vue-press


## 参考になるページ

- VuePress
  https://vuepress.vuejs.org/
- vuejs / vuepress 
  https://github.com/vuejs/vuepress

### チュートリアル

- VuePress で静的ページを作成し GitHub Pages に公開する - Qiita
  https://qiita.com/y4shiro/items/303232d74870d6dbec2d
- VuePress で静的ページを作成し、GitHub Pages に公開する | GitHub Pages
  https://y4shiro.github.io/vue-press/