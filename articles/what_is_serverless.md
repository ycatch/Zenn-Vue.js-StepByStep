---
title: "フロントエンドエンジニアとバックエンドエンジニアで、サーバーレスのイメージが違っている"
emoji: "🤖"
type: "idea" # tech: 技術記事 / idea: アイデア
topics: ["Serverless","サーバーレス"]
published: false
---

サーバーレスアーキテクチャやサーバーレスコンピューティングについて調べていると、フロントエンドエンジニアとバックエンドエンジニアで、そのイメージが違っているような気がしています。

![フロントエンドエンジニアとバックエンドエンジニアによる、サーバーレスのイメージ](https://storage.googleapis.com/zenn-user-upload/8hryi4djhfea4opngehd3kzwhld0)

## フロントエンドエンジニアの場合

フロントエンドアプリから複数のサービスをAPIで呼び出すようなシステム構成を「**サーバーレス**]と呼んでいます。自分でサーバを用意しないという意味が強調されています。

## バックエンドエンジニアの場合

リクエストをトリガーにしてコンテナを起動、レスポンスを返したらコンテナを破棄するという、バックエンド構成を「**サーバーレス**]と呼んでいます。FaaSとかマイクロサービスと同じような文脈で登場します。

本来は、バックエンドの用語なんですが、今どきのReactやVue.jsを使ったWebサービスの開発例などで目に留まりました。

すでに出ている話を、私が調べきれていないだけかもしれません。

## 関連ページ

- 伊藤直也氏が語る、サーバーレスアーキテクチャの性質を解剖する（前編）。QCon Tokyo 2016 － Publickey  
  https://www.publickey1.jp/blog/16/qcon_tokyo_2016.html
- JAMstackってなに？実践に学ぶ高速表示を実現するアーキテクチャの構成 - エンジニアHub
  https://eh-career.com/engineerhub/entry/2019/12/10/103000

- The Serverless Application Framework | Serverless.com
  https://www.serverless.com/
- Ruby on Jets | The Ruby Serverless Framework
  https://rubyonjets.com/

- Nuxt.js + Netlifyで爆速構築するサーバーレス開発入門 - Qiita
  https://qiita.com/isihigameKoudai/items/e3b136e9964f1d30d73d
- 【AWS】簡単なサーバーレスアプリケーションを構築する
  https://zenn.dev/soshimiyamoto/articles/dcb51cbd5725e0
