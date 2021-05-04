---
title: "VutifiyとVee-Validationを使ってみる：Vue.js Step by Step"
emoji: "🤖"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["vuejs","vutifiy","veevalidation"]
published: true
---

このシリーズでは、簡単なところからVue.jsを使い始めて、徐々に本格的に使う手順を記録しています。[前回](./install_vuejs.md)は、Vue.jsを導入して、Vue CLIでつくったアプリをGithub Pagesでデプロイするところまでやりました。

今回は、Vue用UIフレームワークである[Vuetify](https://vuetifyjs.com/en/)と、Formバリデーションライブラリの[Vee-Validation](https://vee-validate.logaretm.com/)を使ってみます。


## Vuetifyを使う

Vue用UIフレームワークには、[Bootstrap](https://bootstrap-vue.org/)や[Tailwind CSS](https://www.vue-tailwind.com/)をベースにしたものなど、いろいろな種類があります。[Vuetify](https://vuetifyjs.com/en/)の特徴は、マテリアルデザインを採用したことです。また、Vue.jsによるアプリケーションフレームワークNuxt.jsでも利用できます。

マテリアルデザインは、Googleが提唱したデザインシステムで、GoogleのアプリやWebサービスなどに採用されています。Vuetifyを使うと、画面のレイアウトやUI部品の配置などを効率よく統一感のある形で進めることができます。

- Vuetify — A Material Design Framework for Vue.js
  https://vuetifyjs.com/ja/

- Vue Material Design Component Framework — Vuetify.js
  https://v2.vuetifyjs.com/ja/


### 導入する

新しいVue.jsプロジェクトをまだ作成していない場合、Vuetifyを導入するには、Vue CLIでライブラリを追加するだけ。途中で、利用するバージョンを聞いてくる場合がありますが、とりあえずデフォルトのものを選んでおきます。

```bash
$ vue create vuetify-app
$ cd vuetify-app
$ vue add vuetify
```

すると、src/plugins/に、vuetify.jsができて、Vuetifyが使えるようになります。


```js:src/plugins/vuetify.js
import Vue from 'vue';
import Vuetify from 'vuetify/lib/framework';

Vue.use(Vuetify);

export default new Vuetify({
});
```

ローカルで動作確認すると、こんな感じになります。

![./images/vutify_and_validation/vuetify.png](https://storage.googleapis.com/zenn-user-upload/tkinuct164dro93mpi0wiewmc485)


### ダークモード

vuetify.jsにオプションを指定するだけで、ダークモードに切り替えることができます。


```js:src/plugins/vuetify.js
import Vue from 'vue'
import Vuetify from 'vuetify/lib'

Vue.use(Vuetify)

export default new Vuetify({
  theme: { dark: true },
})

```

![./images/vutify_and_validation/darkmode.png](https://storage.googleapis.com/zenn-user-upload/ackzi45qqw5ck8intj8diq8f6ll4)



### フォームでテキストを入力する

Vuetifyには、いろいろなUIコンポーネントが用意してあります。

Formで、テキストを入力するとこんな感じです。

![./images/vutify_and_validation/form_input.png](https://storage.googleapis.com/zenn-user-upload/691br6fn9hl8z4kxd6cxd0wm4pcr)

これは、HelloWorld.vueを次のように記述します。

まず、template部分です。formタグに、v-text-fieldタグを記述します。


```html:src\components\HelloWorld.vue
<template>
  <v-container>
    <v-row class="text-left">
      <v-col cols="12">
        <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        />
      </v-col>

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          Hello world
        </h1>

        <p class="subheading font-weight-regular">
          For help and collaboration with other Vuetify developers
        </p>

        <form>
            <v-text-field
                v-model="greeting"
                label="Input"
            ></v-text-field>
            <p>Output: {{ greeting }}</p>
        </form>
      </v-col>

    </v-row>
  </v-container>
</template>
```

script部分では、双方向バインディングを指定します。

```js:src\components\HelloWorld.vue
<script>
  export default {
    name: 'greeting',
    data () {
        return {
            greeting: ''
        }
    }
  }
</script>
```

### 色を指定する

Vuetifyでは、色を指定するのも簡単です。

これは、template部分に「primary」や「secondary」といった役割を指定します。たとえば、src/App.vueのヘッダー部分には、「primary」が指定してあります。

```html:src/App.vue
<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
```

そして、vuetify.jsに役割ごとに色を指定します。vuetify/lib/util/colors をインポートすることで、色名で指定できます。

```js:src/plugins/vuetify.js
import Vue from 'vue';
import Vuetify from 'vuetify/lib/framework';
import colors from 'vuetify/lib/util/colors'

Vue.use(Vuetify);

export default new Vuetify({
    theme: {
        themes: {
          light: {
            primary: colors.blueGrey,
            secondary: colors.grey,
            accent: colors.pink.accent2,
            error: colors.pink.lighten2,
          },
        },
    },
});
```

![./images/vutify_and_validation/color_theme.png](https://storage.googleapis.com/zenn-user-upload/m04o7n4g121x7l6dywkv2jfhsxtf)

## Vee-Validationを使う

Formバリデーションライブラリの[Vee-Validation](https://vee-validate.logaretm.com/)を使うと、Formに入力した値をチェックできます。Vue.jsのバージョンに合わせて、Vee-Validationのバージョンが異なるので注意してください。

- VeeValidate v3 <= Vue.js Ver.2
  https://vee-validate.logaretm.com/v3/
- VeeValidate v4 <= Vue.js Ver.3
  https://vee-validate.logaretm.com/v4/


### 導入する

Vee-Validationの導入は、これもVue CLIでライブラリを追加するだけ。

```bash
$ yarn add vee-validate
```

### プリセットルールを利用する

Vee-Validationは、標準的なルールを[プリセット](https://vee-validate.logaretm.com/v3/guide/rules.html#importing-the-rules)として用意しています。たとえば、次のようなルールを利用できます。

- 必須
- 最小文字数、最大文字数
- email形式

Vee-Validationを使うには、script部分に次のように記述します。ここでは、最大文字数を規定するmaxを読み込んでいます。

```js:src\components\HelloWorld.vue
<script>
  import { ValidationProvider, extend} from "vee-validate";
  import { max } from 'vee-validate/dist/rules';

  extend('max', {
    ...max,
    message: 'Exceeds maximum length'
  });

  export default {
    components: {
        ValidationProvider
    },

    name: 'greeting',
    data () {
        return {
            greeting: ''
        }
    }
  }
</script>
```

それから、template部分のformタグに、ValidationProviderタグを追加します。このとき、最大文字数の値を「3」と設定しています。

```html:src\components\HelloWorld.vue
<form>
    <ValidationProvider v-slot="{ errors }" rules="max:3">
        <v-text-field
            v-model="greeting"
            :error-messages="errors"
            label="Input"
            :success="valid"
        ></v-text-field>
    </ValidationProvider>
    <p>Output: {{ greeting }}</p>
</form>
```

![./images/vutify_and_validation/validation.png](https://storage.googleapis.com/zenn-user-upload/og6lhemtvd1m6flkgun4phh79tqg)



### 日本語メッセージにする

エラーメッセージには、デフォルトで日本語メッセージが利用できます。

![./images/vutify_and_validation/validation_ja.png](https://storage.googleapis.com/zenn-user-upload/a3t704z7yjrcfs3cpl4ilvjvsa66)

これは、HelloWorld.vueのscript部分を次のように記述します。

```js:src\components\HelloWorld.vue
<script>
  import { ValidationProvider, extend, localize } from "vee-validate";
  import { max } from 'vee-validate/dist/rules';
  import ja from 'vee-validate/dist/locale/ja';

  extend('max', max);
  localize('ja', ja);

  export default {
    components: {
        ValidationProvider
    },

    name: 'greeting',
    data () {
        return {
            greeting: ''
        }
    }
  }
</script>
```

## 公開したアプリ

VuetifyとVee-Validationを使ったアプリケーションを、GitHub Pagesで公開しています。

- デモページ(Github Pages)
  https://ycatch.github.io/vuetify_app/
- ソースコード(Github)
  https://github.com/ycatch/vuetify_app


## 参考になるページ

### Vuetify

- Vuetify — A Material Design Framework for Vue.js
  https://vuetifyjs.com/ja/

- テーマの設定 — Vuetify
  https://vuetifyjs.com/ja/features/theme/

- Vuetifyのテーマ(スタイル)変更について - Qiita
  https://qiita.com/yusuke-ka/items/80dd90307e2b5debf5b8


### Vee-Validation

- Vuelidate | A Vue.js model validation library
  https://vuelidate.js.org/

- Handling Forms | VeeValidate
  https://vee-validate.logaretm.com/v3/guide/forms.html

- Localization
  https://vee-validate.logaretm.com/v3/guide/localization.html

#### チュートリアル

- Vue.js のフォームバリデーションライブラリ VeeValidate を評価してみた | DevelopersIO
  https://dev.classmethod.jp/articles/tried-using-veevalidate/

- VeeValidateを使ってVueアプリでバリデーションをする - Qiita
  https://qiita.com/TakahiRoyte/items/843bc5da2732703de1a3

- VeeValidate を使って、vue.jsで簡単にバリデートしてみた - Qiita
  https://qiita.com/youdie/items/417ed2df1bcb6a60001c

- VeeValidateでVue.js用の超便利なバリデーションを実装する | カバの樹
  https://www.kabanoki.net/4955/


#### 入力フォーム

- vue.jsで入力フォームを理解して使いこなす | アールエフェクト
  https://reffect.co.jp/vue/vue-js-input-operate

- Vue.jsでフォームを使おう - Qiita
  https://qiita.com/MariMurotani/items/10702fbcae2997fcae80
