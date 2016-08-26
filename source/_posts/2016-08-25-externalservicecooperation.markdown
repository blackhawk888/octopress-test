---
layout: post
title: "Octopress外部サービス連携"
date: 2016-08-25 21:06:09 +0000
comments: true
categories: ['octopress']
---

### Twitter, Google+, Facebookボタン追加

`_config.yml` に `Twitter`, `Google+`, `Facebook` との連携の設定箇所がある。  
`twitter_tweet_button`、`google_plus_one`、`facebook_like`の値を`true`にすると、 記事の下にそれぞれのシェアリングボタンが出るようになる(デフォルトだとtwitterだけ表示されるようになっている )   
Twitterは`twitter_user`を記入してやることで 自分のツイート等も表記できるように設定できる。

<!-- more -->

### _config.ymal編集

```ruby

# Twitter
twitter_user:
twitter_tweet_button: true

# Google +1
- google_plus_one: false
+ google_plus_one: true
google_plus_one_size: medium

# Google Plus Profile
# Hidden: No visible button, just add author information to search results
googleplus_user:
googleplus_hidden: false

# Facebook Like
- facebook_like: false
+ facebook_like: true
```