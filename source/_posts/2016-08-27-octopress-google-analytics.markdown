---
layout: post
title: "OctopressにGoogle Analytics導入"
date: 2016-08-27 20:05:08 +0000
comments: true
categories: ['octopress', 'google analytics']
---

### Google Analytics設定

Google Analytics(アナリティクス)とは、アクセス解析を行うことができる解析ツール。  
Octopress は、デフォルトで Google Analytics の設定をすることが可能。

<!--more-->

サイトページ内にトラッキングコードと呼ばれるJavaScript コードを埋め込み、
訪問者がサイトへアクセスした際の閲覧情報がGoogle Analyticsサーバへ送信される仕組み。
トラッキング IDとはUA-XXXXXXXX-Xのような文字列で、データの送信先となるアカウントや
プロパティを Google アナリティクス側で特定するためのID。

[Google Analytics](http://www.google.co.jp/intl/ja/analytics/)サイトに行き、ログインまたは
アカウントを作成をクリックしログイン後、`プロパティ名`、`デフォルトのURL`等を設定し保存すると
`トラッキング ID`が表示されるので`_config.yml`に設定する。

### _config.ymlの編集

```ruby
# Google Analytics
google_analytics_tracking_id: UA-XXXXXXXX-X  # <- Google Analytics ID を指定
```

ブログにアクセスされるたびに Google Analyticsで集計される。
